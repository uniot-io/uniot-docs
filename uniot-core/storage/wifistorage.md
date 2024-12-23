# WifiStorage

The `WifiStorage` class extends the [`CBORStorage`](cborstorage.md) class to manage WiFi credentials securely and efficiently within the Uniot project. It handles the storage, retrieval, and validation of WiFi SSIDs and passwords, facilitating seamless network connections. By leveraging CBOR for data serialization, `WifiStorage` ensures that WiFi credentials are stored in a structured and compact format. This class provides methods to set, get, and verify the validity of stored credentials, enabling reliable network configuration and reconnection processes.

**Constructor and Destructor:**

* **`WifiStorage()`**\
  Constructs a `WifiStorage` instance with a predefined file path for storing WiFi credentials.

* **`virtual ~WifiStorage()`**\
  Destructor that ensures proper cleanup.

**Methods:**

* **`const String& getSsid() const`**\
  Retrieves the stored WiFi SSID.

* **`const String& getPassword() const`**\
  Retrieves the stored WiFi password.

* **`void setCredentials(const String& ssid, const String& password)`**\
  Sets the WiFi credentials.

* **`bool isCredentialsValid()`**\
  Checks the validity of the stored WiFi credentials.

* **`virtual bool store() override`**\
  Stores the WiFi credentials to the specified file.

* **`virtual bool restore() override`**\
  Restores WiFi credentials from the specified file.

* **`virtual bool clean() override`**\
  Cleans the stored WiFi credentials.

**Private Members:**

* **`String mSsid`**\
  Stores the WiFi SSID (network name).

* **`String mPassword`**\
  Stores the WiFi password.

**Type Definitions:**

* **`using SchedulerTaskCallback = std::function<void(SchedulerTask &, short)>`**\
  Type alias for a callback function that takes a reference to a `SchedulerTask` and a `short` indicating remaining executions.

* **`using spSchedulerTaskCallback = SharedPointer<SchedulerTaskCallback>`**\
  Type alias for a shared pointer to a `SchedulerTaskCallback`.
