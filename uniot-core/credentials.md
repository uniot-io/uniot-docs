# Credentials

The `Credentials` module is responsible for managing and securing device credentials. Leveraging cryptographic standards and persistent storage mechanisms, the `Credentials` class ensures that device identities and keys are generated, stored, and utilized securely.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`Credentials()`**\
  Constructs a `Credentials` instance, initializing credential data by restoring stored credentials or generating new ones if none exist.

* **`virtual bool store() override`**\
  Stores the current credentials into persistent CBOR storage.

* **`virtual bool restore() override`**\
  Restores credentials from persistent CBOR storage.

* **`void setOwnerId(const String &id)`**\
  Sets the owner identifier for the credentials.

* **`const String &getOwnerId() const`**\
  Retrieves the owner identifier.

* **`const String &getCreatorId() const`**\
  Retrieves the creator identifier.

* **`const String &getDeviceId() const`**\
  Retrieves the device identifier.

* **`const String &getPublicKey() const`**\
  Retrieves the public key in hexadecimal string format.

* **`uint32_t getShortDeviceId() const`**\
  Retrieves a shortened device ID derived from the higher 32 bits of the MAC address for ESP32 or the chip ID for ESP8266.

* **`virtual Bytes keyId() const override`**\
  Retrieves the public key used as the key identifier.

* **`virtual Bytes sign(const Bytes &data) const override`**\
  Signs the provided data using the device's private key.

* **`virtual COSEAlgorithm signerAlgorithm() const override`**\
  Retrieves the cryptographic algorithm used for signing.

**Private Members:**

* **`String mOwnerId`**\
  Stores the owner identifier.

* **`String mCreatorId`**\
  Stores the creator identifier.

* **`String mDeviceId`**\
  Stores the device identifier derived from the MAC address.

* **`Bytes mPrivateKey`**\
  Stores the device's private key.

* **`Bytes mPublicKeyRaw`**\
  Stores the raw public key bytes.

* **`String mPublicKey`**\
  Stores the public key in hexadecimal string format.
