# Guides

The guides are hands-on. Each one takes 20 to 40 minutes, starts from the board you set up in [Getting Started](getting-started.md), and adds the smallest possible change to prove one thing the platform does well: changing a device's behavior without reflashing, letting the device decide on its own, linking devices through events, or teaching scripts a new primitive written in C++.

Follow them in order. Every guide builds its script in the [Sandbox](../platform/sandbox/README.md), runs it in the [Emulator](../platform/sandbox/emulator.md) first, and deploys it only once it behaves. Because the Emulator talks to real dashboards and devices, guides 1, 4, 5 and 6 can be followed almost entirely without extra hardware.

## Start Here

{% content-ref url="getting-started.md" %}
[Getting Started](getting-started.md)
{% endcontent-ref %}

## Learning Path

| #   | Guide                                                       | What you build                                         | What it proves                                      | Extra hardware                |
| --- | ----------------------------------------------------------- | ------------------------------------------------------ | --------------------------------------------------- | ----------------------------- |
| 0   | [Getting Started](getting-started.md)                       | Button, LED and dashboard linked by one event          | Flash once, deploy logic over the air               | None                          |
| 1   | [Scripts Without Reflashing](scripts-without-reflashing.md) | A blink and a press counter, swapped over the air      | Sandbox workflow, task model, persistent scripts    | None                          |
| 2   | [Dim an LED from a Slider](dim-an-led-from-a-slider.md)     | A dashboard slider driving PWM brightness              | Register indices, control widgets, retained events  | LED and resistor              |
| 3   | [A Night Light That Thinks for Itself](night-light.md)      | Light sensor, threshold and LED, decided on the device | Edge logic, publishing only changes, works offline  | Potentiometer or LDR          |
| 4   | Two Devices, One Event                                      | Two peers toggling each other, then a doorbell         | Device-to-device events with no cloud code          | Second board, or the Emulator |
| 5   | Add a Real Sensor with a Custom Primitive                   | A thermostat over a DHT22 exposed as `get_temp`        | Extending scripts from C++, mocking in the Emulator | DHT22                         |
| 6   | Schedule on the Device                                      | A lamp that follows a daily schedule on its own        | Uniot Core time, autonomy, everything combined      | LED or relay                  |

Guides 1 to 6 are coming soon. They will appear in the sidebar as each one is published.

## Hardware-Specific

{% content-ref url="uniot-badge.md" %}
[Uniot Badge](uniot-badge.md)
{% endcontent-ref %}
