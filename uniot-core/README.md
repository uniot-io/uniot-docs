# Uniot Core

Uniot Core is the heartbeat of the Uniot Platform, designed to seamlessly power IoT devices. As a highly optimized open source operating system, it serves as a crucial component, enabling efficient task scheduling, networking, storage management, and more. With its own script sandbox, Uniot Core allows secure and fast direct execution of scripts directly on the device.

## Compatibility

Currently, Uniot Core is optimized for ESP8266 and ESP32 microcontrollers, two of the most popular platforms for IoT development. The decision to base Uniot Core on the Arduino framework and implement it in C++ is rooted in a commitment to accessibility, performance, and community collaboration. Arduino's user-friendly nature, coupled with the efficiency of C++, enables developers to create and scale applications with ease. The platform also benefits from a vast ecosystem of existing libraries and a thriving developer community.

## A Deep Dive into the Architecture

Uniot Core, the backbone of your IoT solutions, uses PlatformIO to organize the project. This structure consists of C++ classes grouped into logical modules, providing a foundation that makes it scalable, easy to understand, and efficient to manage.

### PlatformIO Integration

Uniot Core employs PlatformIO, an open source ecosystem for IoT development, to manage the project's environment. This includes dependency management, streamlined build processes, and integration with various IDEs, ensuring a smooth development experience.

### Modules and Classes

Let's take a closer look at the architecture and what each module entails:

1. **Core:** The Core module holds the fundamental classes of Uniot Core.
   * [**Scheduler**](scheduler/)**:** Task scheduling and execution.
   * [**EventBus**](eventbus/)**:** Contains classes related to event-driven communication between publishers and subscribers.
   * [**Storage**](storage/) For various storage needs, such as CrashStorage and WifiStorage.
   * [**Network**](network/)**:** Covers network devices, schedulers, and configuration.
   * [**Register**](register/)**:** Registering GPIO pins, objects, and managing their associations.
   * [**Utils**](utils/)**:** Utility classes including ArrayBuilder, StringUtils, and more.
   * [**CBORWrapper**](cborwrapper/)**:** Handles CBOR arrays and objects.
   * [**MQTTWrapper**](mqttwrapper/)**:** Classes for MQTT device handling and communication.
   * [**LispWrapper**](lispwrapper/)**:** Includes Lisp helper and expeditor classes.
   * [**Hardware**](hardware/)**:** Classes for hardware interfaces, like Buttons.
   * [**Credentials**](credentials.md) Managing authentication and authorization.
   * _**Logger:**_ Logging utilities.
2. [**AppKit**](appkit/)**:** This module contains classes that form the application toolkit.
   * [**AppKit**](appkit/appkit.md)**:** Main application handling.
   * [**LispDevice**](appkit/lispdevice.md)**:** Integration of Lisp device.
   * [**LispPrimitives**](appkit/lispprimitives.md)**:** Primitive operations within the Lisp environment.
   * [**TopDevice**](appkit/topdevice.md)**:** Handling device-specific debugging functionalities
3. **Uniot**
   * [**Uniot**](uniot.md)**:** Entry point for Uniot initialization.
4. **WebPages**
   * **config.min.html.gz.h:** The compiled Captive Portal configuration page.

For detailed descriptions of each class and module, please navigate to their specific documentation pages.

