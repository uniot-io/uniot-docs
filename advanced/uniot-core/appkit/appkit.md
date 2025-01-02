# AppKit

The `AppKit` class manages MQTT communications, Lisp scripting, network configurations, and event handling, ensuring seamless interaction between hardware and software components.

**Methods:**

* **`static AppKit& getInstance()`**\
  Retrieves the singleton instance of `AppKit`, ensuring a single point of control within the system.

* **`unLisp &getLisp()`**\
  Retrieves a reference to the [`unLisp`](../lispwrapper/unlisp.md) singleton instance, enabling access to the Lisp interpreter.

* **`MQTTKit &getMQTT()`**\
  Retrieves a reference to the [`MQTTKit`](../mqttwrapper/mqttkit.md) instance, facilitating MQTT communications.

* **`const Credentials &getCredentials()`**\
  Retrieves a reference to the [`Credentials`](../credentials.md) object containing device and owner identifiers.

* **`void pushTo(TaskScheduler &scheduler) override`**\
  Integrates the `AppKit`'s tasks with the provided task scheduler, enabling periodic execution of network, MQTT, and Lisp tasks.

* **`void attach() override`**\
  Attaches the `AppKit` to the system by initializing primitives, attaching network and MQTT components, and running stored Lisp scripts.

* **`void registerWithBus(CoreEventBus &eventBus) override`**\
  Registers `AppKit` entities with the [`CoreEventBus`](../eventbus/eventbus.md), enabling event-driven interactions and data channel communications.

* **`void unregisterFromBus(CoreEventBus &eventBus) override`**\
  Unregisters `AppKit` entities from the `CoreEventBus`, cleaning up event listeners and data channels.

* **`void configureNetworkController(const NetworkControllerConfig &config)`**\
  Configures the network controller with the specified settings, setting up buttons and LEDs for network management.

* **`void configureNetworkController(uint8_t pinBtn, uint8_t activeLevelBtn, uint8_t pinLed, uint8_t activeLevelLed, uint8_t maxRebootCount, uint32_t rebootWindowMs)`**\
  Overloaded method to configure the network controller with individual parameters for button and LED pins, reboot count, and reboot window.

**Private Members:**

* **`Credentials mCredentials`**\
  Stores the device and owner credentials used for MQTT communications and topic path construction.

* **`NetworkScheduler mNetwork`**\
  Manages network-related tasks and configurations, ensuring reliable connectivity.

* **`MQTTKit mMQTT`**\
  Manages MQTT communications, handling connections, device registrations, and message processing.

* **`TopDevice mTopDevice`**\
  Instance of [`TopDevice`](topdevice.md) for handling debug-related MQTT interactions and diagnostics.

* **`LispDevice mLispDevice`**\
  Instance of [`LispDevice`](lispdevice.md) for managing Lisp scripting, script execution, and event handling.

* **`UniquePointer<NetworkController> mpNetworkDevice`**\
  Unique pointer to the [`NetworkController`](../network/networkcontroller.md) instance, managing network buttons, LEDs, and reboot configurations.

* **`UniquePointer<CoreCallbackEventListener> mpNetworkEventListener`**\
  Unique pointer to the [`CoreCallbackEventListener`](../eventbus/callbackeventlistener.md) instance, handling network and MQTT connection events.

**Inner Structures:**

* **`struct NetworkControllerConfig`**\
  Configuration structure for setting up the network controller, including button and LED pin numbers, active levels, maximum reboot count, and reboot window duration.
