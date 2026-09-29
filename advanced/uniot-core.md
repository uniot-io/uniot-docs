# Uniot Core

Uniot Core is the open-source firmware framework every Uniot device runs. It connects a device to the platform, keeps it connected, and runs the scripts you deploy to it — so your firmware only has to describe the hardware. It is written for the Arduino framework on ESP8266 and ESP32 boards, and built with PlatformIO.

The source, the full API reference and the examples are in the [uniot-core](https://github.com/uniot-io/uniot-core) repository. This page is a map of it.

## What's inside

### Task scheduler

Runs periodic and one-shot work without blocking the device, with `setTimeout`, `setInterval` and `setImmediate`. See [Task Scheduler](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#1-task-scheduler) in the reference.

### Event system

A publish-subscribe bus the parts of the firmware use to talk to each other without depending on one another. See [Event System](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#2-event-system).

### WiFi management

Connects to the network and reconnects when it drops. Credentials come either from your code or from a captive portal where the device's user enters them. A reset button — or, if you enable it, a quick series of reboots — lets a device that can no longer reach its network start over. See [WiFi Management](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#3-wifi-management).

### UniotLisp scripting

An embedded interpreter runs the scripts you deploy from the platform, so a device's behaviour changes without reflashing. Your firmware decides what scripts can reach: which pins, which buttons, and which functions of your own. See [Scripting](../general-concepts/scripting.md) and [Primitives](../general-concepts/primitives.md) in these docs, and [UniotLisp Scripting](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#4-uniotlisp-scripting) in the reference.

### Storage management

Keeps credentials, configuration, the deployed script and your own data in flash, in the compact CBOR format. See [Storage Management](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#5-storage-management).

### Time management

Keeps the clock in sync over NTP, and saves it so that a device starts with roughly the right time after a reboot, before the network is back. See [Time Management](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#6-time-management).

Messages between the device and the platform travel over MQTT, and the device signs what it publishes with its own Ed25519 key.

## Compatibility

| Family | Boards |
| --- | --- |
| ESP8266 | ESP-12E, ESP-12F, NodeMCU, Wemos D1 Mini |
| ESP32 | ESP32 DevKit, ESP32-C3, ESP32-S2, ESP32-S3 |

## Getting started

Add Uniot Core to a PlatformIO project:

```ini
lib_deps =
    uniot-io/uniot-core@^0.9.0
```

[Getting Started](../guides/getting-started.md) walks through a first project from an empty folder to a device on your dashboard.

## Build flags

Uniot Core is configured with build flags in `platformio.ini`. One is required — `UNIOT_CREATOR_ID`, and the build fails without it. The rest tune logging, storage, memory and the network, and are listed with their defaults in [Build Flags](https://github.com/uniot-io/uniot-core#build-flags) in the repository.

## Examples

Each is a complete PlatformIO project in the repository.

| Example | Shows |
| --- | --- |
| [WittyCloud](https://github.com/uniot-io/uniot-core/tree/master/examples/WittyCloud) | RGB output, a light sensor and a button, all exposed to scripts |
| [My9231Lamp](https://github.com/uniot-io/uniot-core/tree/master/examples/My9231Lamp) | A custom primitive, on a smart bulb with no button or status LED |
| [S20Socket](https://github.com/uniot-io/uniot-core/tree/master/examples/S20Socket) | Relay control and a scriptable GPIO |
| [LispHooks](https://github.com/uniot-io/uniot-core/tree/master/examples/LispHooks) | Powering a sensor on and off around the script that uses it |
| [Buttons](https://github.com/uniot-io/uniot-core/tree/master/examples/Buttons) | Two buttons exposed to scripts, and clearing presses no script has read |

For a complete device, see the [Uniot Badge firmware](https://github.com/uniot-io/uniot-promo-badge-firmware).

## Reference

- [API reference](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#api-reference) — every method, with its parameters
- [Device status](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#device-status) — what a device reports to the platform
- [Troubleshooting](https://github.com/uniot-io/uniot-core/blob/master/docs/reference.md#troubleshooting) — WiFi, memory and upload problems
- [Changelog](https://github.com/uniot-io/uniot-core/blob/master/CHANGELOG.md) — what changed in each release, and what to check before updating a device

Uniot Core is licensed under the [GNU General Public License v3.0](https://github.com/uniot-io/uniot-core/blob/master/LICENSE).
