---
hidden: true
---

# Scripts Without Reflashing

<!-- AUTHOR: Skeleton, outline only (guide 1 of 6). Expand each section into full prose, verify every listing in the Emulator and on a board, then remove `hidden: true` and add the page to SUMMARY.md after Getting Started. -->

You flashed the firmware once in [Getting Started](getting-started.md). In this guide you never touch the USB cable again: you write three different scripts, test each in the browser, and push each to the board over the air. About 20 minutes.

## What You'll Build

- A blinking LED, built from blocks and tested in the Emulator before it ever reaches the board.
- An SOS pattern that replaces the blink with one click, showing that the old behavior is simply gone.
- A press counter that reports through `print`, introducing the logs you will debug with from now on.
- Proof that a persistent script survives a power cycle.

This is the everyday loop of the platform: the board is generic, the behavior is a script, and changing it costs seconds. Read more in [Edge Logic Deployment](../foundations/edge-logic-deployment.md).

## Prerequisites

- The board from [Getting Started](getting-started.md), online and authorized. No extra parts.
- No firmware change. The onboard LED is digital output `0` and the BOOT/FLASH button is button `0`.

## Step 1: Blink from the Emulator to the Board

### Build the Script

<!-- AUTHOR: prose for creating a new script in the Sandbox; verify the exact "new script" control. -->

In the Visual Editor: a **task** block (iterations `0`, interval `500`), a **set variable** `state` to **not** `state`, and a **digital write** of index `0` with `state`.

{% code title="blink.lisp" lineNumbers="true" %}

```lisp
;;; begin-user-library
; (defjs dwrite (pin state)) ;-> Bool
;;; end-user-library

(define state ())

(task 0 500 '
 (list
  (setq state (not state))
  (dwrite 0 state)))
```

{% endcode %}

What the script does:

- `state` flips on every pass.
- `dwrite 0` writes it to the onboard LED.

### Run It in the Emulator

- Press **Compile**, select your device in the sidebar, then the play button or Ctrl+Enter (Cmd+Enter on Mac).
- The Digital Write card's LED blinks every half second. The header shows the device name, meaning the Emulator checked the script against the device's registers.
- Link: [Emulator](../platform/sandbox/emulator.md#quick-start).

### Deploy

Press **Deploy** in the Emulator header. It sends the script and closes the window.

{% hint style="success" %}
**Checkpoint** — the onboard LED blinks (ESP8266: inverted, but blinking is blinking).
{% endhint %}

## Step 2: Replace It with SOS

### A Finite Task

- Explain that a task with a non-zero iteration count runs that many times and stops, and that **task pass** (`#t_pass`) counts down from `iterations - 1` to `0` ([Special blocks](../platform/sandbox/visual-editor/special.md#task-pass)).
- 21 passes at 250 ms: passes 20 to 15 blink short, 14 to 6 blink long, 5 to 0 blink short.

{% code title="sos.lisp" lineNumbers="true" %}

```lisp
;;; begin-user-library
; (defjs dwrite (pin state)) ;-> Bool
;;; end-user-library

(task 21 250 '
 (dwrite 0
  (if (and (< #t_pass 15) (> #t_pass 5))
   (not (= (% #t_pass 3) 0))
   (= (% #t_pass 2) 1))))
```

{% endcode %}

<!-- AUTHOR: verify the pattern timing in the Emulator with Debug mode on; check whether a single-expression task body needs the (list ...) wrapper. -->

In the Visual Editor: **task** (iterations `21`, interval `250`), **digital write** with an **if** block choosing between two **remainder** comparisons of **task pass**.

### Watch It Finish

- Run it. Turn on **Debug** (bug icon) to see each `dwrite` call light the card in order; the run slows to one call per 300 ms.
- When the task ends the window title changes to **Finished**.
- Deploy. The LED plays SOS once and stays off. The blink from Step 1 is gone: a device runs one script.

{% hint style="success" %}
**Checkpoint** — three short, three long, three short, then dark.
{% endhint %}

{% hint style="info" %}
In the Emulator an infinite task stops after 9,999 iterations and intervals are waited in real time. On a device, `0` iterations really means forever. See [Limits](../platform/sandbox/emulator.md#limits).
{% endhint %}

## Step 3: Count Button Presses

{% code title="counter.lisp" lineNumbers="true" %}

```lisp
;;; begin-user-library
; (defjs bclicked (button_id)) ;-> Bool
; (defjs dwrite (pin state)) ;-> Bool
;;; end-user-library

(define count 0)

(task 0 50 '
 (if (bclicked 0)
  (list
   (setq count (+ count 1))
   (dwrite 0 (= (% count 2) 1))
   (print count))))
```

{% endcode %}

What the script does:

- `bclicked 0` is true once per press and clears itself.
- The LED shows whether the count is odd.
- `print` sends the count to the logs.

In the Visual Editor: **task**, **if** with **button clicked**, **change variable** by `1`, **digital write**, **print**.

### Read the Logs

- In the Emulator, click the Button Clicked card and watch timestamped lines appear in the **Logs** panel ([Logs](../platform/sandbox/emulator.md#logs)).
- The **Logger** pane in the Sandbox is different: it traces which primitives were called and what they answered.
- After deploying, the same lines appear on the device page under **Logs**. Link [Debugging Scripts](../general-concepts/scripting.md#debugging-scripts).

{% hint style="success" %}
**Checkpoint** — each press of BOOT/FLASH adds a line to the device's **Logs** tab and toggles the LED on odd counts.
{% endhint %}

## Step 4: Survive a Reboot

- Deploy the counter as a persistent script. <!-- AUTHOR: exact label of the persistent/volatile option in the Deploy flow. -->
- Unplug the board, plug it back in. Once the status LED goes dark the script is running again: press the button, the log line appears.
- Explain Volatile vs Persistent from [Script Persistence](../general-concepts/scripting.md#script-persistence): saved to flash, checksum verified on boot, a broken script does not block boot.

{% hint style="success" %}
**Checkpoint** — the counter works after a power cycle without any deploy.
{% endhint %}

## Troubleshooting

<!-- AUTHOR: bold-symptom paragraphs. Planned entries: -->

- The play button is disabled: the Sandbox shows **Recompile required**; press **Compile** first.
- "Undefined symbol" on compile: hand-written code is missing a `defjs` line in the user library block ([User Library Block](../general-concepts/primitives.md#user-library-block)).
- The Emulator flags "Registers are out of bounds": the script uses an index the selected device did not register; check the device's **Registers** tab.
- Deployed but nothing happens: device page **Logs** tab, then [Debugging Scripts](../general-concepts/scripting.md#debugging-scripts).

## What's Next

{% content-ref url="dim-an-led-from-a-slider.md" %}
[Dim an LED from a Slider](dim-an-led-from-a-slider.md)
{% endcontent-ref %}

{% content-ref url="../general-concepts/scripting.md" %}
[Scripting](../general-concepts/scripting.md)
{% endcontent-ref %}

{% content-ref url="../platform/sandbox/emulator.md" %}
[Emulator](../platform/sandbox/emulator.md)
{% endcontent-ref %}
