---
hidden: true
---

# Dim an LED from a Slider

<!-- AUTHOR: Skeleton, outline only (guide 2 of 6). Expand into full prose, verify on ESP8266 and ESP32, then remove `hidden: true` and add to SUMMARY.md after Scripts Without Reflashing. -->

A dashboard slider sets the brightness of an LED through PWM. Along the way you make the one and only firmware change of this series, learn how firmware exposes hardware to scripts, and see the broker remember the slider for a device that reboots. About 30 minutes.

## What You'll Build

- One new line in `main.cpp` that registers an analog output.
- A script that pops a `brightness` event and writes it with `awrite`.
- A **Slider** widget with **Retain** on, tested against the Emulator before the LED ever lights.
- A power cycle after which the LED comes back at the last slider position.

Why it matters: scripts address hardware by logical index, not by GPIO, so the same script runs on any board whose firmware registers the same indices. See [The Register System](../general-concepts/primitives.md#the-register-system).

## Prerequisites

- The board from [Getting Started](getting-started.md).
- An LED and a 220 Ω resistor on a breadboard. <!-- AUTHOR: pick and verify pins: ESP8266 D5/GPIO14, ESP32 GPIO4; onboard LED as a fallback where PWM-capable. -->
- One firmware change, described in Step 1.

## Step 1: Register an Analog Output

### Wire the LED

<!-- AUTHOR: two or three sentences per board; anode to the GPIO through the resistor, cathode to GND. Tabs only if pins differ. -->

### Add One Line to main.cpp

{% code title="main.cpp (excerpt)" lineNumbers="true" %}

```c++
#define PIN_LED_PWM 14  // AUTHOR: per-board value

void setup() {
  // ... everything from Getting Started ...
  Uniot.registerLispAnalogOutput(PIN_LED_PWM);  // (awrite 0 value)
  Uniot.begin();
}
```

{% endcode %}

- Explain: this is a capability, not logic. Firmware declares what the hardware can do; scripts decide what it does. Each primitive has its own index namespace, so analog output `0` and digital output `0` can be different pins ([Registering GPIO Pins](../general-concepts/primitives.md#registering-gpio-pins)).
- Reflash with `pio run --target upload`.

{% hint style="success" %}
**Checkpoint** — the device page's **Registers** tab lists analog output `0` on your pin.
{% endhint %}

<!-- AUTHOR: verify `awrite` range on ESP32. Docs say 0-1023; Arduino-ESP32 `analogWrite` defaults to 8-bit. Check the uniot-core implementation and state the real range or a clamp. -->

## Step 2: Write the Script

{% code title="dimmer.lisp" lineNumbers="true" %}

```lisp
;;; begin-user-library
; (defjs awrite (pin value)) ;-> Bool
; (defjs bclicked (button_id)) ;-> Bool
;;; end-user-library

(define brightness 0)

(task 0 100 '
 (list
  (if (is_event 'brightness)
   (list
    (setq brightness (pop_event 'brightness))
    (awrite 0 brightness)))
  (if (bclicked 0)
   (push_event 'brightness 0))))
```

{% endcode %}

What the script does:

- Every 100 ms it checks for a `brightness` event and writes the value to analog output `0`.
- Event payloads are numbers, which is exactly what `awrite` wants ([push event](../platform/sandbox/visual-editor/special.md#push-event)).
- The physical button publishes `brightness 0`, so the dashboard slider follows it too.

In the Visual Editor: **task**, **if** with **is event**, **set variable** from **pop event**, **analog write**, a second **if** with **button clicked** and **push event**.

## Step 3: Add the Slider and Test Without Hardware

- Open **Dashboard**, enter **Edit Mode**, add a **Slider**, name it, bind it to event `brightness`, set its range, enable **Retain** ([Widget Configuration](../platform/dashboard.md#widget-configuration)). <!-- AUTHOR: exact names of the min/max/step settings. -->
- Back in the Sandbox: **Compile**, select the device, play. The Emulator window floats, so open the **Dashboard** page next to it and drag the slider: the Analog Write gauge follows. Events between the dashboard and the Emulator go through the real broker ([Events](../platform/sandbox/emulator.md#events)).
- Press **Deploy** from the Emulator header.

{% hint style="success" %}
**Checkpoint** — dragging the slider dims the real LED; pressing BOOT/FLASH pulls the slider to zero.
{% endhint %}

## Step 4: Reboot and Watch Retain Work

- Set the slider to about half. Unplug the board, plug it back in.
- The LED returns to half brightness with no interaction: the broker stored the last retained `brightness` and replayed it when the device reconnected ([Retained Messages](../api-reference/mqtt-convention.md#retained-messages)).
- The same happens in the Emulator: on a fresh run the retained value seeds the queue, so the first `is_event` check already finds the slider's value.
- Contrast: turn **Retain** off, repeat, and the LED stays dark after a reboot until someone touches the slider.

{% hint style="success" %}
**Checkpoint** — after a power cycle the LED comes back at the last slider level.
{% endhint %}

## Troubleshooting

<!-- AUTHOR: bold-symptom paragraphs. Planned entries: -->

- LED never lights: check polarity and the pin against the **Registers** tab.
- LED only fully on or off: the value range does not match; see the range note in Step 1.
- Slider moves but nothing happens: event name mismatch between the widget and the script; event names are case-sensitive.
- The Emulator says "Registers are out of bounds": the selected device was not reflashed with the new line.

## What's Next

{% content-ref url="night-light.md" %}
[A Night Light That Thinks for Itself](night-light.md)
{% endcontent-ref %}

{% content-ref url="../general-concepts/primitives.md" %}
[Primitives](../general-concepts/primitives.md)
{% endcontent-ref %}

{% content-ref url="../platform/dashboard.md" %}
[Dashboard](../platform/dashboard.md)
{% endcontent-ref %}
