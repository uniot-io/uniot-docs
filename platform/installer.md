# Firmware Installer

[install.uniot.io](https://install.uniot.io) installs and updates the [Uniot Badge](../guides/uniot-badge.md) firmware from your browser. It tells you which firmware the badge is running and which is available, and when it's done it checks that the new version has started. You don't need to install anything on your computer.

{% hint style="info" %}
The installer has firmware for the Uniot Badge only. To put Uniot Core on another board, build your own firmware with PlatformIO, as in [Getting Started](../guides/getting-started.md).
{% endhint %}

## What you need

- **Desktop Chrome, Edge or Opera.** The installer talks to the badge over Web Serial, which Firefox, Safari and phone browsers don't support.
- **A USB-C cable that carries data.** With a charge-only cable, the badge never appears in the browser's list.
- **On Linux, access to serial ports.** On most distributions this means your user is in the `dialout` group (`uucp` on Arch). Log out and back in after adding yourself to it.

## Install or update

1. Open [install.uniot.io](https://install.uniot.io), plug the badge in, and press **Connect**.
2. Choose the badge in the list your browser shows. The installer asks the badge what it's running and shows it next to the latest release:
   - **On the badge** — the installed version and radio build, or that no Uniot firmware answered: a new board, or one running something else.
   - **Available** — the latest release, with a link to what's new in it.
3. Choose the **WiFi radio** build — see [Which radio build](#which-radio-build). The build the badge already has is marked **installed**.
4. Press the main button. It says what it will do: **Update to** a newer version, **Reinstall** the one the badge has, or **Install** on a badge running anything else.

The installer downloads the firmware, checks it against its checksum, writes it, and restarts the badge. Keep the badge plugged in until it has finished. When the badge reports the new version, the installer says so: *The badge is running 1.0.0 · Compatible*.

Nothing is written until you press the main button. **Disconnect** releases the badge at any point before that.

## What an update keeps

An update keeps the badge's WiFi settings, its identity on the platform and its script. When it's done, the badge reconnects and carries on, with nothing to set up again. The same is true when you switch radio builds or reinstall.

A new board, or one that you've erased, starts with nothing stored. After installing:

1. Join the WiFi network named `UNIOT-…` from your phone or computer.
2. On the page that opens, enter your WiFi details and your Uniot account ID.
3. When the badge is online, authorize it on the **Devices** page — see [Authorize the Device](../guides/getting-started.md#authorize-the-device).

## Which radio build

Some ESP32-C3 modules can't hold a WiFi connection at the chip's full transmit power, and nothing on the board tells you which ones.

| Build | Transmit power | Use it when |
| --- | --- | --- |
| **Compatible** | 8.5 dBm | By default. It works on every badge, at a shorter range. It's what badges ship with. |
| **Full range** | 19.5 dBm | You want more range and your badge's radio copes. If the badge never connects, install Compatible instead. |

Switching between them keeps the badge's settings.

## Erasing

**Erase everything first** is off unless you tick it. It removes the badge's WiFi settings, script and identity. Afterwards the badge has to be set up and authorized again, like a new one. You only need it for a board that previously ran other firmware.

## Testing the hardware

**Test the hardware instead** installs a small test program in place of the firmware. It checks all four peripherals without a network or an account. The ring sweeps and the badge buzzes, then the ring follows your hand as you move it over the distance sensor. If a red dot chases around the ring instead, the sensor didn't answer. The button drives the vibration motor throughout.

When you're done, press **Install the firmware** to go back. The test doesn't touch the badge's settings, so it comes back as it was.

## The serial console

Below the installer, the serial console shows the badge's log while it is connected. Choose how much to show with the level filter, **Restart** the badge, or **Copy**, **Save** or **Clear** the log. If something goes wrong, the log is the first thing to look at, and the thing to attach when you ask for help.

## Troubleshooting

**The badge isn't in the browser's list.** Try another cable. Many USB-C cables only carry power. On Linux, check that your user can open serial ports (see [What you need](#what-you-need)).

**The port is in use.** Another program has the badge open. Close any serial monitor, the Arduino IDE or PlatformIO's monitor, or another browser tab connected to it, then try again.

**Couldn't start the installation.** The badge didn't switch into the mode that accepts new firmware. Unplug it, then hold the **BOOT** button on its ESP32-C3 board while you plug it back in. Release the button and try again. The chip's bootloader can always accept new firmware this way, even when the firmware on it doesn't start.

**This is a different board.** The installer only has firmware for the Uniot Badge, which is built on an ESP32-C3.

**The badge keeps restarting after an update.** Watch the serial console. If it doesn't settle, install again, and tick **Erase everything first** if it still doesn't.

**The badge never connects to WiFi.** If it runs the **Full range** build, install **Compatible**. Otherwise, reset its WiFi settings: click the button four times, then press and hold it. The badge opens its `UNIOT-…` network again, where you can enter the details anew. Powering it off and on five times in quick succession does the same.

## Building your own

The installer also works for a badge you've built yourself on a breadboard, if it uses the badge's pins. The released firmware has them built in. It finds boards through the USB-serial chips common on ESP32 development boards, not only through the C3's built-in USB. If you've moved any pins, build the firmware from source instead — see the [firmware repository](https://github.com/uniot-io/uniot-promo-badge-firmware#building-one-without-a-badge).
