# Getting Started

This guide takes you from a bare ESP board to a working IoT device in about 20 minutes. You will flash the Uniot Core firmware once, connect the device to your account, deploy a script to it over the air, and control it from a browser dashboard.

## What You'll Build

A device whose physical button, onboard LED, and browser dashboard all talk through a single `led` event:

- Press the physical button — the onboard LED toggles, and the dashboard reflects it.
- Toggle a switch on the dashboard — the onboard LED follows.

None of this logic is compiled into the firmware. You flash generic firmware once; the behavior comes from a small script deployed to the device over the air, and devices, scripts, and dashboards all communicate through events. This is Uniot's core idea — read more in [Edge Logic Deployment](../foundations/edge-logic-deployment.md).

## Prerequisites

- A supported board. This guide provides ready-to-use configurations for **NodeMCU-class ESP8266** and **ESP32 DevKit** boards; any other ESP8266/ESP32 board works with minor pin tweaks.
- A USB **data** cable (some charging cables carry no data).
- [PlatformIO](https://platformio.org/) installed — either the VSCode extension or the CLI.
- A Uniot account — [Get Early Access](https://forms.fillout.com/t/k1LDnvkgvPus). Once you are in, copy your **account ID** from your profile page (it is also shown on the Add-new-device screen). You will need it in Step 1 or Step 2, depending on the path you choose.

## Step 1: Flash the Firmware

### Create a Project

Create a new PlatformIO project (via the IDE or `pio project init`) — or open an existing one — and replace its `platformio.ini` and `src/main.cpp` with the files below.

### Configure platformio.ini

{% tabs %}
{% tab title="ESP8266 (NodeMCU)" %}
{% code title="platformio.ini" lineNumbers="true" %}

```ini
[env:nodemcuv2]
platform = espressif8266
framework = arduino
board = nodemcuv2
monitor_speed = 115200
board_build.filesystem = littlefs

lib_deps =
    uniot-io/uniot-core@^0.8.1

build_unflags =
    -std=gnu++11

build_flags =
    -std=gnu++17
    -D UNIOT_CREATOR_ID=\"UNIOT\"
    -D UNIOT_USE_LITTLEFS=1
    -D UNIOT_LOG_ENABLED=1
    -D UNIOT_LOG_LEVEL=4
    -D MQTT_MAX_PACKET_SIZE=2048
```

{% endcode %}

Using a different ESP8266 board? Change `board` accordingly (e.g. `d1_mini`, `esp12e`).
{% endtab %}

{% tab title="ESP32 (DevKit)" %}
{% code title="platformio.ini" lineNumbers="true" %}

```ini
[env:esp32doit-devkit-v1]
platform = espressif32
framework = arduino
board = esp32doit-devkit-v1
monitor_speed = 115200
board_build.filesystem = littlefs

lib_deps =
    uniot-io/uniot-core@^0.8.1

build_unflags =
    -std=gnu++11

build_flags =
    -std=gnu++17
    -D UNIOT_CREATOR_ID=\"UNIOT\"
    -D UNIOT_USE_LITTLEFS=1
    -D UNIOT_LOG_ENABLED=1
    -D UNIOT_LOG_LEVEL=4
    -D MQTT_MAX_PACKET_SIZE=2048
```

{% endcode %}

Using a different ESP32 board? Change `board` accordingly (e.g. `esp32dev`).
{% endtab %}
{% endtabs %}

`UNIOT_CREATOR_ID` is **required** — the build fails without it. The full list of build flags is described in [Build Flags](../advanced/uniot-core.md#build-flags). For ESP32-C3 boards (extra USB flags) and projects targeting several boards at once, see [Multi-Environment Configuration](../advanced/uniot-core.md#multi-environment-configuration).

### Write main.cpp

Both files below are complete — pick your board's tab and copy it as is.

{% tabs %}
{% tab title="ESP8266 (NodeMCU)" %}
{% code title="main.cpp" lineNumbers="true" %}

```c++
#include <Uniot.h>

// NodeMCU and most ESP8266 boards:
// GPIO0 = FLASH button (pressed = LOW)
// GPIO2 = onboard LED (lit when LOW - inverted)
#define PIN_BUTTON 0
#define BTN_ACTIVE_LEVEL LOW
#define PIN_LED 2
#define LED_ACTIVE_LEVEL LOW

void setup() {
  // Option A: hardcoded credentials - uncomment and fill in:
  // Uniot.configWiFiCredentials("YourSSID", "YourPassword");
  // Uniot.configUser("your_account_id");
  // Option B: captive portal - leave them commented.

  // Blink connection status on the onboard LED.
  Uniot.configWiFiStatusLed(PIN_LED, LED_ACTIVE_LEVEL);

  // WiFi reset button; also exposed to scripts as (bclicked 0).
  Uniot.configWiFiResetButton(PIN_BUTTON, BTN_ACTIVE_LEVEL, true);

  // Let scripts drive the LED as digital output 0: (dwrite 0 ...).
  Uniot.registerLispDigitalOutput(PIN_LED);

  Uniot.begin();
}

void loop() {
  Uniot.loop();
}
```

{% endcode %}

{% hint style="info" %}
The onboard LED on GPIO2 is inverted: when a script or the dashboard turns it "on", the LED goes dark. Prefer non-inverted behavior? Wire an external LED with a resistor from GPIO2 to GND and set `LED_ACTIVE_LEVEL` to `HIGH`.
{% endhint %}
{% endtab %}

{% tab title="ESP32 (DevKit)" %}
{% code title="main.cpp" lineNumbers="true" %}

```c++
#include <Uniot.h>

// ESP32 DevKit (DoIt v1):
// GPIO0 = BOOT button (pressed = LOW)
// GPIO2 = onboard LED (lit when HIGH)
#define PIN_BUTTON 0
#define BTN_ACTIVE_LEVEL LOW
#define PIN_LED 2
#define LED_ACTIVE_LEVEL HIGH

void setup() {
  // Option A: hardcoded credentials - uncomment and fill in:
  // Uniot.configWiFiCredentials("YourSSID", "YourPassword");
  // Uniot.configUser("your_account_id");
  // Option B: captive portal - leave them commented.

  // Blink connection status on the onboard LED.
  Uniot.configWiFiStatusLed(PIN_LED, LED_ACTIVE_LEVEL);

  // WiFi reset button; also exposed to scripts as (bclicked 0).
  Uniot.configWiFiResetButton(PIN_BUTTON, BTN_ACTIVE_LEVEL, true);

  // Let scripts drive the LED as digital output 0: (dwrite 0 ...).
  Uniot.registerLispDigitalOutput(PIN_LED);

  Uniot.begin();
}

void loop() {
  Uniot.loop();
}
```

{% endcode %}

{% hint style="info" %}
Some ESP32 boards (e.g. the official ESP32-DevKitC) have no onboard user LED. If yours doesn't, wire an LED with a resistor from GPIO2 to GND.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Decide how the device will get your WiFi credentials before uploading:**

- **Option A: Hardcoded credentials** — uncomment the two config lines in `setup()` and fill in your WiFi SSID, password, and Uniot account ID.
- **Option B: Captive portal** — leave them commented; you will provision the device from your phone in Step 2.
{% endhint %}

While connecting, Uniot Core blinks the connection status on the LED; once connected, the LED goes dark and your scripts own it (if WiFi drops, the core temporarily takes it back). Note that scripts address hardware by logical index, not GPIO number: the button is exposed as `(bclicked 0)` and the LED as digital output `0` — see [the register system](../general-concepts/primitives.md#the-register-system) for how indices work and [WiFi Management](../advanced/uniot-core.md#wifi-management) for details on the WiFi subsystem.

### Upload

Connect the board via USB and run:

```bash
pio run --target upload
```

Or press the upload arrow in the PlatformIO toolbar of VSCode.

{% hint style="success" %}
**Checkpoint** — run `pio device monitor`: you should see Uniot Core log lines. The onboard LED shows the connection state:

- **Slow blink** — setup (Access Point) mode, waiting to be provisioned (Option B continues in Step 2)
- **Medium blink** — connecting to your WiFi
- **Fast blink** — error
- **Brief flash, then dark** — connected (what you should see with Option A)
{% endhint %}

## Step 2: Connect the Device to Your Account

Both options end in the same place: the device is online under your account and appears on the **Devices** page. (If you mix them, hardcoded values win — `configWiFiCredentials()` overwrites stored values on every boot.)

{% tabs %}
{% tab title="Option A: Hardcoded credentials" %}
You already provided everything before flashing. The device connects on boot — the status LED goes dark — and registers with your account ID. Continue to authorization below.
{% endtab %}

{% tab title="Option B: Captive portal" %}
**Start the wizard.** Open the **Devices** page on the platform and click **Add new device**. The screen shows step-by-step instructions along with your account ID.

{% hint style="info" %}
On an iPhone or Mac, copy your account ID **before** joining the device's WiFi — the captive portal opens in a separate window, and this page won't be reachable until you disconnect. (Your account ID is also available on your profile page.)
{% endhint %}

**Join the device's network.** Power the device and connect your phone or laptop to the WiFi network named `UNIOT-xxxxxx`.

**Provision it.** In the portal that opens, enter your account ID, pick your home WiFi (**Scan Networks**), type its password, and press **Connect**.

{% hint style="info" %}
Your WiFi credentials are used only on the device itself, only to connect it to the Internet. After pressing **Connect**, allow up to 15 seconds — the portal shows no progress while the device connects and registers.
{% endhint %}
{% endtab %}
{% endtabs %}

### Authorize the Device

New devices are not trusted automatically. Open the **Devices** page, switch to the **Unauthorized** tab, select your device, and click **Authorize** to bind it to your account.

<!-- AUTHOR: verify the exact button label on the Devices page -->

{% hint style="success" %}
**Checkpoint** — your device appears on the Devices page with the status **Online**. If it doesn't, see [Troubleshooting](#troubleshooting).
{% endhint %}

## Step 3: Deploy Your First Script

Open the **Sandbox** page. Every new account comes with a welcome script called **"My First Script"** — open it. The script is built from visual blocks, which compile to this UniotLisp code, executed directly on the device:

```lisp
;;; begin-user-library
;; This block describes the library of user functions.
;; So the editor knows that your device implements it.
;
; (defjs bclicked (button_id)) ;-> Bool
; (defjs dwrite (pin state)) ;-> Bool
;
;;; end-user-library

(define state ())

(setq state ())

; Runs the task every '50' ms. Since 'times' is '0',
; it runs indefinitely. The context is released after
; each run, allowing other processes to run smoothly.
(task 0 50 '
 (list
  ; If the button '0' is clicked, emit an event 'led' to toggle state.
  (if
   (bclicked 0)
   (list
    (push_event 'led
     (not state))))
  ; When the 'led' event is triggered, set 'state' to the received
  ; value and write to pin '0', driving the LED accordingly.
  (if
   (is_event 'led)
   (list
    (setq state
     (pop_event 'led))
    (dwrite 0 state)))))
```

What the script does:

- **State variable** — `state` starts as `false` and tracks whether the LED is on.
- **Task** — `(task 0 50 '...)` runs the body every 50 ms, forever (`times` is `0`). Every script is built around this [task model](../general-concepts/scripting.md#task-based-execution-model).
- **Button check** — when `(bclicked 0)` reports a click, the script publishes the `led` event with the toggled value. Events travel through MQTT, so the dashboard (and other devices) hear them too.
- **Event handler** — when a `led` event arrives, the script saves its value into `state` and writes it to digital output `0` via `dwrite`. Indices like `0` refer to [registered pins](../general-concepts/primitives.md#the-register-system), not raw GPIO numbers.

The firmware from Step 1 already provides both indices: `bclicked 0` is your BOOT/FLASH button, and digital output `0` is the onboard LED.

{% hint style="info" %}
No hardware at hand? You can run this script in the [Emulator](../platform/sandbox/emulator.md) and interact with virtual components instead.
{% endhint %}

To deploy: with the script open, press **Deploy**, select the device you authorized in Step 2, and confirm. The [Sandbox](../platform/sandbox/README.md) page describes the full development workflow.

<!-- AUTHOR: verify the exact deploy control labels in the Sandbox UI -->

{% hint style="success" %}
**Checkpoint** — press the **BOOT/FLASH** button on the board: the onboard LED toggles with each press (remember, inverted on ESP8266). Nothing happens? Open your device's page, check the **Logs** tab, and see [Debugging Scripts](../general-concepts/scripting.md#debugging-scripts).
{% endhint %}

## Step 4: Control It from the Dashboard

Open the **Dashboard** page. A pre-made dashboard called **"My First Dashboard"** was also created for your account. It contains two widgets, both bound to the `led` event:

- **Switch** — publishes the `led` event each time you toggle it.
- **LED** — subscribes to the `led` event and reflects its current value.

With the script deployed, the device, the script, and the dashboard form one loop around the `led` event:

- **Press the physical button** — the script publishes `led` with the toggled value to the MQTT broker. The broker delivers it back to the script (which updates `state` and drives the LED via `dwrite`) and to the dashboard (whose widgets update).
- **Toggle the Switch widget** — the dashboard publishes the same `led` event, and the script receives and handles it in exactly the same way.

The device doesn't treat the dashboard as anything special — everything simply speaks events. See [Dashboard](../platform/dashboard.md) for widgets and layout editing.

{% hint style="success" %}
**Checkpoint** — it works in both directions: pressing the physical button flips the Switch and LED widgets, and toggling the Switch flips the onboard LED (ESP8266: "on" = unlit).
{% endhint %}

## Troubleshooting

**Upload fails or no serial port appears.** Hold the BOOT/FLASH button while PlatformIO prints "Connecting…"; make sure the CH340/CP2102 USB driver is installed; try adding `upload_speed = 115200` to `platformio.ini`.

**I don't see the `UNIOT-xxxxxx` network.** The device already has stored WiFi credentials, so it skips Access Point mode. Clear them: quick-press the button 5–8 times, then hold it for 3–5 seconds — or power-cycle the device 5 times in quick succession (a built-in recovery mechanism, active by default).

**I can't join the device's network.** Forget the `UNIOT-xxxxxx` network on your phone or laptop and connect to it again.

**The device never appears under Unauthorized.** Usually a wrong or missing account ID (Option A: `configUser()`; Option B: the portal field) or wrong WiFi credentials. Watch the serial monitor for connection errors, and allow up to 15 seconds after the portal's **Connect**.

**The LED keeps blinking.** A medium or fast blink that never stops means wrong credentials or a router out of range. Hold the button for 3–5 seconds to force a reconnect attempt, or clear the WiFi config (see above) and redo Step 2.

**The script is deployed but nothing happens.** Open your device's page and check the **Logs** tab for script errors, the **Script** tab to confirm the deployment, and the **Registers** tab to confirm pin indices — then see [Debugging Scripts](../general-concepts/scripting.md#debugging-scripts).

## What's Next

You now have the full loop — firmware, over-the-air scripts, and a dashboard. Keep going:

{% content-ref url="../general-concepts/scripting.md" %}
[Scripting](../general-concepts/scripting.md)
{% endcontent-ref %}

{% content-ref url="../general-concepts/primitives.md" %}
[Primitives](../general-concepts/primitives.md)
{% endcontent-ref %}

{% content-ref url="../platform/dashboard.md" %}
[Dashboard](../platform/dashboard.md)
{% endcontent-ref %}

{% content-ref url="../foundations/edge-logic-deployment.md" %}
[Edge Logic Deployment](../foundations/edge-logic-deployment.md)
{% endcontent-ref %}

{% content-ref url="uniot-badge.md" %}
[Uniot Badge](uniot-badge.md)
{% endcontent-ref %}
