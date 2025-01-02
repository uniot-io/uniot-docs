# CallbackMQTTDevice

The `CallbackMQTTDevice` class extends the [`MQTTDevice`](mqttdevice.md) class by incorporating callback functionalities, enabling customized handling of incoming MQTT messages. This class allows to define specific behaviors in response to received messages, facilitating dynamic and responsive device interactions.

**Methods:**

* **`CallbackMQTTDevice(Handler handler)`**\
  Constructs a `CallbackMQTTDevice` instance with a specified handler function for processing incoming MQTT messages.

* **`void handle(const String &topic, const Bytes &payload) override`**\
  Overrides the abstract `handle` method from `MQTTDevice` to invoke the assigned callback function with the incoming message data.

**Private Members:**

* **`Handler mHandler`**\
  Stores the user-defined callback function responsible for processing incoming MQTT messages.
