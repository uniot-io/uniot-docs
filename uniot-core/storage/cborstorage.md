# CBORStorage

The `CBORStorage` class extends the [`Storage`](storage.md) class to handle structured data using CBOR (Concise Binary Object Representation). This allows for efficient serialization and deserialization of complex data structures, making it suitable for storing configuration data and other structured information.

**Constructor and Destructor:**

* **`CBORStorage(const String &path)`**:
  Constructs a `CBORStorage` instance with a specified file path.

* **`virtual ~CBORStorage()`**:
  Destructor that ensures proper cleanup.

**Methods:**

* **`CBORObject &object()`**:
  Retrieves a reference to the internal CBOR object.

* **`virtual bool store() override`**:
  Stores the CBOR data to the specified file.

* **`virtual bool restore() override`**:
  Restores CBOR data from the specified file.

* **`virtual bool clean() override`**:
  Cleans the CBOR data by resetting the CBOR object and removing the file.

**Protected Members:**

* **`CBORObject mCbor`**:
  Instance of `CBORObject` used for managing structured CBOR data.

**Type Definitions:**

* **`using SchedulerTaskCallback = std::function<void(SchedulerTask &, short)>`**:
  Type alias for a callback function that takes a reference to a `SchedulerTask` and a `short` indicating remaining executions.

* **`using spSchedulerTaskCallback = SharedPointer<SchedulerTaskCallback>`**:
  Type alias for a shared pointer to a `SchedulerTaskCallback`.
