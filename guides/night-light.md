---
hidden: true
---

# A Night Light That Thinks for Itself

<!-- AUTHOR: Skeleton, outline only (guide 3 of 6). Expand into full prose, verify sensor pins on both boards, then remove `hidden: true` and add to SUMMARY.md after Dim an LED from a Slider. The hidden `development-board.md` (Witty Cloud, built-in LDR + RGB LED) can become a board tab here. -->

A light sensor, a threshold, and an LED. The device reads, decides and acts on its own; the dashboard only watches the value and tunes the threshold. At the end you switch the WiFi off and the night light keeps working. About 40 minutes.

## What You'll Build

- An analog input registered in firmware and read with `aread`.
- A script that turns the LED on when it gets dark, without sending anything anywhere.
- A `light` event published only when the reading changes by more than a step, and a display widget showing it.
- A `threshold` slider on the dashboard, retained, that the script reads back.
- A demonstration that none of this needs the network.

This is [Edge Logic Deployment](../foundations/edge-logic-deployment.md) in one page: the logic lives on the device, the cloud is an observer.

## Prerequisites

- The board and LED from [Dim an LED from a Slider](dim-an-led-from-a-slider.md).
- A potentiometer, or an LDR with a 10 kΩ resistor as a voltage divider. <!-- AUTHOR: ESP8266 `A0` (1 V range on bare modules, 3.3 V on NodeMCU); ESP32 GPIO34 and attenuation. -->
- One firmware line, described in Step 1.

## Step 1: Register the Analog Input

{% code title="main.cpp (excerpt)" lineNumbers="true" %}

```c++
#define PIN_LDR A0  // AUTHOR: per-board value

void setup() {
  // ... everything from the previous guides ...
  Uniot.registerLispAnalogInput(PIN_LDR);  // (aread 0)
  Uniot.begin();
}
```

{% endcode %}

{% hint style="success" %}
**Checkpoint** — the **Registers** tab shows analog input `0`.
{% endhint %}

## Step 2: Read and Log the Sensor

- First script: read `(aread 0)` every 200 ms and `print` it.
- Emulator: turn the Analog Read knob and watch the **Logs** panel. The script sees the new value about half a second after you stop turning ([Analog Read](../platform/sandbox/emulator.md#analog-read)).
- Device: deploy, cover the sensor, watch the device page **Logs** tab. Note the range you observe; you will pick the threshold from it.

{% hint style="success" %}
**Checkpoint** — covering the sensor changes the printed value.
{% endhint %}

## Step 3: Decide on the Device

{% code title="night-light.lisp" lineNumbers="true" %}

```lisp
;;; begin-user-library
; (defjs aread (pin)) ;-> Int
; (defjs dwrite (pin state)) ;-> Bool
;;; end-user-library

(define threshold 300)
(define light 0)
(define last_sent -100)

(task 0 200 '
 (list
  (setq light (aread 0))
  (dwrite 0 (< light threshold))
  (if (> (abs (- light last_sent)) 20)
   (list
    (setq last_sent light)
    (push_event 'light light)))
  (if (is_event 'threshold)
   (setq threshold (pop_event 'threshold)))))
```

{% endcode %}

What the script does:

- Reads the sensor and drives the LED from a local comparison. No message leaves the device for this.
- Publishes `light` only when the reading moved by more than 20 since the last publish.
- Accepts a new `threshold` from the dashboard.

In the Visual Editor: **task**, **set variable** from **analog read**, **digital write** with a **comparison**, **if** with **math operation** (absolute) and **arithmetic**, **push event**, **if** with **is event** and **pop event**.

<!-- AUTHOR: present this as three incremental edits (decide, publish changes, accept threshold) rather than one listing, with a checkpoint after each. -->

### Why Publish Only Changes

- A paragraph on bandwidth, broker load, and dashboard noise: five readings per second times every device is not a plan. Edge filtering is the device doing the thinking.

## Step 4: Watch and Tune from the Dashboard

- Add a display widget bound to `light`. <!-- AUTHOR: exact widget name (gauge, value, chart). -->
- Add a **Slider** bound to `threshold` with **Retain** on.
- Emulator first: knob on one side, slider on the other, LED card in between. Then deploy from the header.

{% hint style="success" %}
**Checkpoint** — the widget follows the sensor in steps; moving the slider changes where the LED switches.
{% endhint %}

## Step 5: Pull the Plug on WiFi

- Switch the router off, or carry the board out of range. The status LED starts blinking as Uniot Core tries to reconnect; the night light keeps switching with the sensor.
- Bring the network back. The device reconnects, the widget catches up, the retained threshold is still in force.
- The payoff paragraph: contrast with an imperative setup where the cloud sends "turn on" and a dead link means a dark room ([Imperative model](../foundations/edge-logic-deployment.md)).

<!-- AUTHOR: confirm that the WiFi status LED and the script LED are different pins in this guide's wiring, so the reconnect blink does not mask the night light. -->

{% hint style="success" %}
**Checkpoint** — the LED keeps reacting to the sensor with the network down.
{% endhint %}

## Troubleshooting

<!-- AUTHOR: bold-symptom paragraphs. Planned entries: -->

- Readings stuck at 0 or the maximum: divider wiring, or the wrong ADC pin for the board.
- Readings jitter and the widget updates constantly: raise the step from 20.
- The slider has no effect: event name mismatch, or the slider's range does not overlap the readings.
- Nothing after reconnect: the device's **Logs** tab; a script error stops the interpreter.

## What's Next

{% content-ref url="two-devices-one-event.md" %}
[Two Devices, One Event](two-devices-one-event.md)
{% endcontent-ref %}

{% content-ref url="../foundations/edge-logic-deployment.md" %}
[Edge Logic Deployment](../foundations/edge-logic-deployment.md)
{% endcontent-ref %}
