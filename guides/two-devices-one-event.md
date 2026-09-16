---
hidden: true
---

# Two Devices, One Event

<!-- AUTHOR: Skeleton, outline only (guide 4 of 6). Expand into full prose, verify with a real second board and with the Emulator as the second peer, then remove `hidden: true` and add to SUMMARY.md after the night light guide. -->

Two peers run the Getting Started script. Press the button on one and the LED on both toggles, and the dashboard follows. Then you give them different roles by deploying different scripts, without changing a line of firmware or writing anything in the cloud. About 30 minutes, no extra hardware if you use the Emulator as the second peer.

## What You'll Build

- A second peer: another ESP board, or the Emulator standing in for one.
- The same script on both, proving scripts are portable across boards.
- A doorbell: one peer publishes `ring`, the other blinks on it.
- The dashboard as a third peer with a **Push Button** and an **LED** widget.

Why it matters: every device, dashboard and Emulator in your account shares one event bus. Devices do not know about each other; they only know event names ([Event Communication](../api-reference/mqtt-convention.md#event-communication)).

## Prerequisites

- The board from [Getting Started](getting-started.md).
- Either a second ESP board with the Getting Started firmware, or nothing: the Emulator publishes and receives real events ([Events](../platform/sandbox/emulator.md#events)).
- No firmware change. A mixed ESP8266 and ESP32 pair is a good demonstration of portability.

{% hint style="warning" %}
Pushed events are real. If other devices in your account already react to `led`, rename the event in this guide's scripts.
{% endhint %}

## Step 1: Bring Up the Second Peer

{% tabs %}
{% tab title="Second board" %}
Repeat Steps 1 and 2 of [Getting Started](getting-started.md) on the second board and authorize it. Both devices show **Online** on the **Devices** page.
{% endtab %}

{% tab title="Emulator as the second device" %}
Open **My First Script** in the Sandbox, press **Compile**, and run it without selecting a device. Leave the floating window open; it keeps running while you browse.
{% endtab %}
{% endtabs %}

## Step 2: One Script, Two Peers

- The welcome script from Getting Started already does the job: it pushes `led` on a click and pops `led` into the LED. Deploy it to device A; peer B runs it too.
- Press the button on A: the LED on A toggles, and so does the LED on B (or the Digital Write card). The dashboard **Switch** follows.
- Click the Emulator's Button Clicked card, or press the button on B: device A toggles.
- Explain what happened: `push_event` publishes on the account-wide event topic, every device subscribes to it, and the Emulator publishes with sender type `emulator`. Scripts are deployed per device; events are shared.

{% hint style="success" %}
**Checkpoint** — either button toggles both LEDs and the dashboard Switch.
{% endhint %}

## Step 3: Different Roles, Same Firmware

### The Bell Button (peer A)

- Push `ring` with value `1` on click. Nothing else.

### The Bell (peer B)

{% code title="bell.lisp" lineNumbers="true" %}

```lisp
;;; begin-user-library
; (defjs dwrite (pin state)) ;-> Bool
;;; end-user-library

(define blinks 0)

(task 0 100 '
 (list
  (if (is_event 'ring)
   (list
    (pop_event 'ring)
    (setq blinks 6)))
  (if (> blinks 0)
   (list
    (dwrite 0 (= (% blinks 2) 0))
    (setq blinks (- blinks 1))))))
```

{% endcode %}

What the script does:

- On `ring` it loads a countdown of 6 half-periods, which plays as three blinks.
- The event is popped so it does not fire again.

In the Visual Editor: **task**, **if** with **is event** and **pop event**, **set variable**, **if** with **comparison**, **digital write** with **remainder**, **change variable** by `-1`.

- Deploy the two scripts to the two peers. Point out that both boards still run the identical firmware; the roles came from scripts.

{% hint style="success" %}
**Checkpoint** — a press on A makes B blink three times.
{% endhint %}

## Step 4: The Dashboard as a Third Peer

- Add a **Push Button** widget bound to `ring` and an **LED** widget bound to `ring`.
- Press the widget: B rings. Press A's button: the LED widget flashes.
- One sentence: the dashboard is not special; it is one more publisher and subscriber.

{% hint style="success" %}
**Checkpoint** — three peers, one event name, no configuration linking them.
{% endhint %}

### Going Further

- A third board running the bell script joins without a change anywhere. A paragraph, no steps.

## Troubleshooting

<!-- AUTHOR: bold-symptom paragraphs. Planned entries: -->

- Only one device reacts: check both are authorized under the same account and both run a script that handles the event.
- The Emulator does not receive device events: confirm the run was started after the device was online. <!-- AUTHOR: verify Emulator receives device-originated events when started without a device selected. -->
- B rings repeatedly: the event was not popped.
- Retained values from an earlier guide interfere: clear them by publishing once with **Retain** off, or use fresh event names.

<!-- AUTHOR: confirm that events from one device reach the account's other devices with no grouping setup (firmware subscribes groups/all/event/+). -->

## What's Next

{% content-ref url="custom-primitive-sensor.md" %}
[Add a Real Sensor with a Custom Primitive](custom-primitive-sensor.md)
{% endcontent-ref %}

{% content-ref url="../api-reference/mqtt-convention.md" %}
[MQTT Convention](../api-reference/mqtt-convention.md)
{% endcontent-ref %}
