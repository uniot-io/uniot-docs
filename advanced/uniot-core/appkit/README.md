# AppKit

The `AppKit` module serves as the central orchestrator within the Uniot Core. It manages MQTT communications, Lisp scripting, network configurations, event handling, ensuring seamless interaction between hardware and software components.

### Components

[**AppKit**](appkit.md)

Serves as the central orchestrator within the Uniot Core. It manages MQTT communications, Lisp scripting, network configurations, and event handling, ensuring seamless interaction between hardware and software components.

[**LispDevice**](lispdevice.md)

Handles script execution, event processing, and error management, providing a bridge between Lisp scripts and MQTT communications. By managing the storage and execution of Lisp scripts, `LispDevice` enables dynamic and programmable behaviors for IoT devices.

[**LispPrimitives**](lispprimitives.md)

Encapsulates a set of functions that implement fundamental hardware interactions as Lisp primitives. These primitives allow Lisp scripts to control hardware resources dynamically, such as digital and analog I/O operations and button interactions. Providing these primitives enables flexible and programmable hardware control through Lisp scripting.

[**TopDevice**](topdevice.md)

Extends the [`MQTTDevice`](../mqttwrapper/mqttdevice.md) class to handle device-specific debugging functionalities. It subscribes to debug topics, processes top-related and memory-related requests, and publishes relevant diagnostic information using the [`TaskScheduler`](../scheduler/taskscheduler.md). This class enables real-time monitoring and debugging of device performance and resource utilization.
