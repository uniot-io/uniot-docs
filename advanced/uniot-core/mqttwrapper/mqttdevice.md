# MQTTDevice

The `MQTTDevice` class provides essential functionalities for subscribing to MQTT topics, publishing messages, and handling incoming messages. By encapsulating the core MQTT operations, `MQTTDevice` simplifies the integration of MQTT communication.

**Methods:**

* **`const String &getDeviceId() const`**\
  Retrieves the unique identifier of the device.

* **`const String &getOwnerId() const`**\
  Retrieves the unique identifier of the device owner.

* **`const String &subscribe(const String &topic)`**\
  Subscribes the device to a specific MQTT topic.

* **`const String &subscribeDevice(const String &subTopic)`**\
  Subscribes the device to a device-specific subtopic.

* **`const String &subscribeGroup(const String &groupId, const String &subTopic)`**\
  Subscribes the device to a group-specific subtopic.

* **`bool unsubscribe(const String &topic)`**\
  Unsubscribes the device from a specific MQTT topic.

* **`virtual void syncSubscriptions() = 0`**\
  Synchronizes the device's subscriptions. This pure virtual method must be implemented by derived classes to reconstruct subscriptions that depend on credentials or other dynamic factors.

* **`void unsubscribeFromAll()`**\
  Unsubscribes the device from all currently subscribed MQTT topics.

* **`bool isSubscribed(const String &topic)`**\
  Checks if the device is subscribed to a specific MQTT topic.

* **`bool isTopicMatch(const String &storedTopic, const String &incomingTopic) const`**\
  Determines if an incoming topic matches a stored subscription topic, supporting MQTT wildcards.

* **`void publish(const String &topic, const Bytes &payload, bool retained = false, bool sign = false)`**\
  Publishes a message to a specific MQTT topic with options for message retention and signing.

* **`void publishDevice(const String &subTopic, const Bytes &payload, bool retained = false, bool sign = false)`**\
  Publishes a message to a device-specific subtopic.

* **`void publishGroup(const String &groupId, const String &subTopic, const Bytes &payload, bool retained = false, bool sign = false)`**\
  Publishes a message to a group-specific subtopic.

* **`void publishEmptyDevice(const String &subTopic)`**\
  Publishes an empty (null) message to a device-specific subtopic, typically used for signaling or state changes.

**Private Members:**

* **`IterableQueue<String> mTopics`**\
  Queue managing the list of subscribed MQTT topics for the device.

* **`MQTTKit *mpKit`**\
  Pointer to the central `MQTTKit` instance managing MQTT connections and communications.

* **`static const String sEmptyString`**\
  A static empty string used as a default return value when device or owner IDs are not available.
