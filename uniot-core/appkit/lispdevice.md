# LispDevice

The `LispDevice` class handles script execution, event processing, and error management, providing a bridge between Lisp scripts and MQTT communications. By managing the storage and execution of Lisp scripts, `LispDevice` enables dynamic and programmable behaviors for IoT devices.

**Constructor:**

* **`LispDevice()`**\
  Constructs a `LispDevice` instance, initializes storage, and sets up event listeners for Lisp message handling.

**Methods:**

* **`virtual void syncSubscriptions() override`**\
  Subscribes to MQTT topics related to script execution and event handling, ensuring that the device listens to relevant messages.

* **`unLisp &getLisp()`**\
  Retrieves a reference to the [`unLisp`](lispwrapper/unlisp.md) singleton instance, enabling access to the Lisp interpreter.

* **`void runStoredCode()`**\
  Restores stored Lisp scripts from persistent storage and executes them if persistence is enabled and no errors have occurred.

* **`bool store()`**\
  Stores the current Lisp script, persistence flag, and checksum to persistent storage, ensuring that scripts can be restored after a reboot or power cycle.

* **`virtual void onEventReceived(unsigned int topic, int msg) override`**\
  Handles events received from the `unLisp` module, such as message errors, logs, additions, and new events, processing them accordingly.

* **`virtual void handle(const String &topic, const Bytes &payload) override`**\
  Processes incoming MQTT messages by delegating to specific handlers based on the topic, handling script commands and events.

* **`void handleScript(const Bytes &payload)`**\
  Processes incoming script messages, executing new Lisp scripts if they differ from the currently stored script or if persistence is disabled.

* **`void handleEvent(const Bytes &payload)`**\
  Processes incoming event messages, forwarding them to the `unLisp` module for further handling.

**Private Members:**

* **`uint32_t mChecksum`**\
  Stores the checksum of the currently stored Lisp script to detect changes and ensure script integrity.

* **`bool mPersist`**\
  Indicates whether the Lisp script should be persisted to storage, allowing it to be restored after a reboot or power cycle.

* **`bool mFailedWithError`**\
  Flags whether the last script execution failed with an error, preventing further script executions until resolved.

* **`String mTopicScript`**\
  Stores the MQTT topic string for receiving script execution requests.

* **`String mTopicEvents`**\
  Stores the MQTT topic string for receiving event-related messages.
