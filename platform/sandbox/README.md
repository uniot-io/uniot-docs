# Sandbox

The Sandbox is where you write the scripts your devices run: build them from blocks or write them as code, try them in the [Emulator](emulator.md), and deploy them to a device — all in the browser, without reflashing anything.

{% hint style="info" %}
The Sandbox needs a desktop browser. On a phone, a script shows its block diagram but can't be edited.
{% endhint %}

## Layout

- **The editor**, on the left, takes most of the screen. In **Blockly** mode it is the [Visual Editor](visual-editor/); in **Advanced** mode it is a code editor for [UniotLisp](../../advanced/uniot-lisp/language-description.md).
- **The code preview**, on the right, shows the UniotLisp code your blocks generate, read-only. Show or hide it with **Ctrl+P**; the Sandbox remembers your choice.
- **The [Logger](logger.md)**, below the preview, shows the result of the last compile or emulator run.

A new script starts with one block already in place: a [task](../../general-concepts/scripting.md) that repeats every 500 ms. Put what the device should do inside it.

## Visual Editor vs. Code Editor

The switch at the top of the Sandbox moves between the two ways of writing a script.

- **Blockly** — build the script from blocks in the [Visual Editor](visual-editor/). The code is generated from them.
- **Advanced** — write the UniotLisp code yourself, or paste it in. Switching from Blockly to Advanced takes the code the blocks generated, so you can start from blocks and continue by hand.

The two don't stay in sync. Code you write in Advanced mode isn't turned back into blocks, and **switching back to Blockly replaces it with the code the blocks generate**, so the Sandbox asks before it does. Once you've written a script by hand, keep it in Advanced mode. The Sandbox remembers the mode a script was saved in and opens it that way.

The code editor in Advanced mode has three tools of its own, which appear at its top right when you move the pointer over it:

| Tool | Shortcut | What it does |
| --- | --- | --- |
| **Parinfer** | Shift+Alt+Space | Off by default. When on, it keeps the parentheses balanced as you type, working them out from your indentation. |
| **Beautify** | Shift+Space | Re-indents the code |
| **Keyboard shortcuts** | Ctrl+Alt+H | Lists every shortcut the editor has |

{% hint style="info" %}
A script created before the Sandbox began tracking how a script was written asks, the first time you open it, whether it was built with blocks or written as code, so it can open in the right mode.
{% endhint %}

## Compile, emulate, deploy

The buttons at the top right take a script from the editor to a device.

**Compile** (Ctrl+B) turns the script into the code a device runs. The result appears in the [Logger](logger.md). If compiling fails, the error is shown at the top of the Sandbox, and in Advanced mode the code editor marks the line and underlines the expression that failed.

After you change a script, **Recompile required** appears, and emulating or deploying waits until you compile again — so what you test and deploy is always what you see.

**Emulate** (Ctrl+Enter) runs the compiled script in the [Emulator](emulator.md), a simulated device in the browser. **Terminate** (Ctrl+Enter again) stops it.

**Deploy** sends the compiled script to a device, which runs it straight away and keeps it across reboots. A device that is offline receives the script when it next connects. It goes to the device selected in the sidebar's device list — the button's tooltip names it — and if none is selected, the Sandbox asks which one. If the script uses a primitive the device doesn't have, or the device hasn't reported its primitives yet, the Sandbox says so and asks before deploying.

**Save** (Ctrl+S) stores the script. **Unsaved changes** appears while there is something to save, and leaving the Sandbox with unsaved changes asks whether to save them, discard them, or stay.

## The selected device

Selecting a device in the sidebar does more than choose where Deploy sends a script. The Sandbox compiles for that device:

- The [Primitives](visual-editor/primitives.md) category in the Visual Editor offers the functions that device's firmware provides.
- Compiling uses the device's memory limits, so a script that fits here fits there.

Without a selected device, the Primitives category offers the five standard ones — digital and analog read and write, and button clicks — and compiling uses default memory limits.

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| Ctrl+S | Save |
| Ctrl+B | Compile |
| Ctrl+Enter | Emulate, or terminate the emulator |
| Ctrl+P | Show or hide the code preview |

On a Mac, use Cmd instead of Ctrl.

## Typical workflow

1. **Select your device** in the sidebar, so the Sandbox knows its primitives.
2. **Create a script** and build its logic with blocks, or switch to Advanced and write it.
3. **Compile** it, and fix anything the [Logger](logger.md) reports.
4. **Emulate** it to check its behavior before it touches hardware.
5. **Deploy** it to the device.
6. **Save** it, to change or deploy it again later.
