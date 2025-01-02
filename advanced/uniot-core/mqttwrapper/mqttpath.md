# MQTTPath

The `MQTTPath` class is responsible for constructing and managing MQTT topic paths based on device and owner credentials. It ensures that MQTT topics are organized, secure, and adhere to a consistent naming convention. By centralizing the logic for topic path construction, `MQTTPath` simplifies the management of device-specific, group-specific, and public MQTT topics.

**Methods:**

* **`MQTTPath(const Credentials &credentials)`**\
  Constructs an `MQTTPath` instance using the provided device credentials.

* **`const String& getDeviceId() const`**\
  Retrieves the unique identifier of the device.

* **`const String& getOwnerId() const`**\
  Retrieves the unique identifier of the device owner.

* **`String buildDevicePath(const String &topic) const`**\
  Constructs a device-specific MQTT topic path by appending the provided subtopic to the base device path.

* **`String buildGroupPath(const String& groupId, const String &topic) const`**\
  Constructs a group-specific MQTT topic path by incorporating the group identifier and the provided subtopic.

* **`String buildPublicPath(const String &topic) const`**\
  Constructs a public MQTT topic path by appending the provided topic to the public prefix.

* **`const Credentials *getCredentials() const`**\
  Retrieves the associated `Credentials` object.

**Member Variables:**

* **`const String mPrefix`**\
  Stores the base prefix used for constructing MQTT topic paths, ensuring a standardized topic structure across the system.

* **`const Credentials *mpCredentials`**\
  Pointer to the `Credentials` object containing device and owner identifiers, used for building secure and organized topic paths.
