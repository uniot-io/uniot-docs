# Uniot Core

Uniot Core is the heartbeat of the Uniot platform, designed to seamlessly power IoT devices. As a highly optimized open source operating system, it serves as a crucial component, enabling efficient task scheduling, networking, storage management, and more. With its own script sandbox, Uniot Core allows secure and fast direct execution of scripts directly on the device.

## Compatibility

Currently, Uniot Core is optimized for ESP8266 microcontrollers, with plans to extend support to ESP32 controllers. The decision to base Uniot Core on the Arduino framework and implement it in C++ is rooted in a commitment to accessibility, performance, and community collaboration. Arduino's user-friendly nature, coupled with the efficiency of C++, enables developers to create and scale applications with ease. The platform also benefits from a vast ecosystem of existing libraries and a thriving developer community.

## A Deep Dive into the Architecture

Uniot Core, the backbone of your IoT solutions, uses PlatformIO to organize the project. This structure consists of C++ classes grouped into logical modules, providing a foundation that makes it scalable, easy to understand, and efficient to manage.

### PlatformIO Integration

Uniot Core employs PlatformIO, an open source ecosystem for IoT development, to manage the project's environment. This includes dependency management, streamlined build processes, and integration with various IDEs, ensuring a smooth development experience.

### Modules and Classes

Let's take a closer look at the architecture and what each module entails:

1. **Core:** The Core module holds the fundamental classes of Uniot Core.
   * [**Scheduler**](scheduler/)**:** Task scheduling and execution.
   * **Broker:** Contains classes related to message brokering, such as Publisher, Subscriber, and more.
   * **Storage:** For various storage needs, such as CrashStorage and WifiStorage.
   * **Network:** Covers network devices, schedulers, and configuration.
   * [**Utils**](utils/)**:** Utility classes including ArrayBuilder, StringUtils, and more.
   * **CBORWrapper:** Handles CBOR arrays and objects.
   * **MQTTWrapper:** Classes for MQTT device handling and communication.
   * **LispWrapper:** Includes Lisp helper and expediter classes.
   * **Hardware:** Classes for hardware interfaces, like Buttons.
   * _**Credentials:**_ Managing authentication and authorization.
   * _**Logger:**_ Logging utilities.
   * _**PinMap:**_ Handling of pin mapping.
2. **AppKit:** This module contains classes that form the application toolkit.
   * **AppKit:** Main application handling.
   * **LispDevice:** Integration of Lisp device.
   * **LispPrimitives:** Primitive operations within the Lisp environment.
3. **Platforms:**
   * **Board-WittyCloud:** Platform-specific configuration for the Witty Cloud board.
4. **Uniot**
   * **Uniot:** Entry point for Uniot initialization.
5. **WebPages**
   * **config.min.html.gz.h:** The compiled Captive Portal configuration page.

For detailed descriptions of each class and module, please navigate to their specific documentation pages.

