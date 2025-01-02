# MQTTKit

The `MQTTKit` class manages connections to the MQTT broker, oversees multiple [`MQTTDevice`](mqttdevice.md) instances, handles message publishing and subscribing, and ensures secure and efficient communication through COSE message handling. By integrating with network and time synchronization events, `MQTTKit` provides a robust and reliable foundation for MQTT-based interactions.

**Methods:**

* **`MQTTKit(const Credentials &credentials, CBORExtender infoExtender = nullptr)`**\
  Constructs an `MQTTKit` instance with the specified credentials and an optional CBOR extender for additional information.
  * **`credentials`** (`const Credentials &`): Reference to a [`Credentials`](../credentials.md) object containing device and owner identifiers.
  * **`infoExtender`** (`CBORExtender`, optional): A function to extend CBOR messages with additional information.

* **`~MQTTKit()`**\
  Destructs the `MQTTKit` instance, handling cleanup and deregistration of all associated devices.

* **`void setServer(const char *domain, uint16_t port)`**\
  Sets the MQTT broker server's domain and port for establishing connections.

* **`void addDevice(MQTTDevice &device)`**\
  Registers an `MQTTDevice` instance with the `MQTTKit`, enabling it to participate in MQTT communications.

* **`void removeDevice(MQTTDevice &device)`**\
  Deregisters an `MQTTDevice` instance from the `MQTTKit`, removing it from MQTT communications.

* **`const MQTTPath &getPath()`**\
  Retrieves the [`MQTTPath`](mqttpath.md) instance used for constructing MQTT topic paths.

* **`void renewSubscriptions()`**\
  Re-subscribes all registered devices to their respective MQTT topics, ensuring that subscriptions are up-to-date.

* **`virtual void pushTo(TaskScheduler &scheduler) override`**\
  Integrates the `MQTTKit`'s MQTT task with the provided task scheduler, enabling periodic execution of MQTT operations.

* **`virtual void attach() override`**\
  Placeholder method for attaching the `MQTTKit` to the scheduler or system. Currently not implemented.

* **`virtual void onEventReceived(unsigned int topic, int msg) override`**\
  Handles events received by the `MQTTKit`, such as network connectivity changes and time synchronization events, to manage MQTT connection cycles.

**Private Members:**

* **`const Credentials *mpCredentials`**\
  Pointer to the `Credentials` object containing device and owner identifiers.

* **`MQTTPath mPath`**
  Instance of `MQTTPath` used for constructing MQTT topic paths based on credentials.

* **`CBORExtender mInfoExtender`**\
  Function pointer for extending CBOR messages with additional information.

* **`PubSubClient mPubSubClient`**\
  Instance of the [`PubSubClient`](https://github.com/uniot-io/uniot-pubsubclient) library used for MQTT communications.

* **`bool mNetworkConnected`**\
  Flag indicating the current network connection status.

* **`int mConnectionId`**\
  Identifier for tracking MQTT connection attempts and sessions.

* **`WiFiClient mWiFiClient`**\
  WiFi client instance used for establishing network connections.

* **`ClearQueue<MQTTDevice *> mDevices`**\
  Queue managing all registered `MQTTDevice` instances.

* **`TaskScheduler::TaskPtr mTaskMQTT`**\
  Pointer to the scheduled MQTT task responsible for managing MQTT operations.
