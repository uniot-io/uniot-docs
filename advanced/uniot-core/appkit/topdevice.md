# TopDevice

The `TopDevice` class extends the [`MQTTDevice`](../mqttwrapper/mqttdevice.md) class to handle device-specific debugging functionalities. It subscribes to debug topics, processes top-related and memory-related requests, and publishes relevant diagnostic information using the [`TaskScheduler`](../scheduler/taskscheduler.md). This class enables real-time monitoring and debugging of device performance and resource utilization.

**Constructor:**

* **`TopDevice()`**\
  Constructs a `TopDevice` instance and initializes member variables.

**Methods:**

* **`virtual void syncSubscriptions() override`**\
  Subscribes to device-specific debug topics for top and memory requests.

* **`void setScheduler(const TaskScheduler& scheduler)`**\
  Assigns a reference to a `TaskScheduler` instance for managing scheduled tasks.

* **`virtual void handle(const String& topic, const Bytes& payload) override`**\
  Processes incoming MQTT messages by delegating to specific handlers based on the topic.

* **`void handleTop()`**\
  Gathers and publishes top-related diagnostic information, such as task statuses and uptime.

* **`void handleMem()`**\
  Gathers and publishes memory-related diagnostic information, such as available heap memory.

**Private Members:**

* **`const TaskScheduler* mpScheduler`**\
  Pointer to the `TaskScheduler` instance used for managing scheduled tasks.

* **`String mTopicTopAsk`**\
  Stores the MQTT topic string for top-related debug requests.

* **`String mTopicMemAsk`**\
  Stores the MQTT topic string for memory-related debug requests.
