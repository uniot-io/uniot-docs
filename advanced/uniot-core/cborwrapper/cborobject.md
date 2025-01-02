# CBORObject

The `CBORObject` class provides a flexible and intuitive interface for creating, manipulating, and parsing CBOR data structures. It abstracts the complexities of the underlying CBOR library (`cn-cbor`), enabling developers to work with CBOR maps, arrays, integers, strings, and binary data effortlessly. The class also supports nested structures, allowing for the creation of complex and hierarchical data representations.

**Constructor and Destructor:**

* **`CBORObject()`**\
  Constructs an empty `CBORObject` instance. Initializes a new CBOR object, preparing it for data manipulation. Sets the initial state to not dirty and creates an empty CBOR map.

* **`CBORObject(Bytes buf)`**\
  Constructs a `CBORObject` instance from a given byte buffer. Initializes the CBOR object by decoding the provided byte buffer. If decoding fails, it initializes an empty CBOR map and logs a warning.

* **`CBORObject(const CBORObject &)`**\
  Copy constructor (not implemented). Disabled to prevent unintended copying. Logs a warning if attempted.

* **`CBORObject& operator=(const CBORObject &)`**\
  Copy assignment operator (not implemented). Disabled to prevent unintended assignment. Logs a warning if attempted.

* **`virtual ~CBORObject()`**\
  Destructor that cleans up the CBOR object. Frees allocated resources and resets internal pointers to prevent memory leaks.

**Data Manipulation:**

* **`CBORObject &put(int key, int value)`**\
  Inserts or updates an integer value with an integer key.

* **`CBORObject &put(int key, uint64_t value)`**\
  Inserts or updates an unsigned integer value with an integer key.

* **`CBORObject &put(int key, int64_t value)`**\
  Inserts or updates a 64-bit integer value with an integer key.

* **`CBORObject &put(int key, const char *value)`**\
  Inserts or updates a string value with an integer key.

* **`CBORObject &put(int key, const uint8_t *value, int size)`**\
  Inserts or updates a byte array with an integer key.

* **`CBORObject &put(const char *key, int value)`**\
  Inserts or updates an integer value with a string key.

* **`CBORObject &put(const char *key, uint64_t value)`**\
  Inserts or updates an unsigned integer value with a string key.

* **`CBORObject &put(const char *key, int64_t value)`**\
  Inserts or updates a 64-bit integer value with a string key.

* **`CBORObject &put(const char *key, const char *value)`**\
  Inserts or updates a string value with a string key.

* **`CBORObject &put(const char *key, const uint8_t *value, int size)`**\
  Inserts or updates a byte array with a string key.

* **`Array putArray(int key)`**\
  Creates or retrieves a CBOR array associated with an integer key.

* **`Array putArray(const char *key)`**\
  Creates or retrieves a CBOR array associated with a string key.

* **`CBORObject putMap(const char *key)`**\
  Creates or retrieves a CBOR map associated with a string key.

* **`CBORObject getMap(int key) const`**\
  Retrieves a CBOR map associated with an integer key.

* **`CBORObject getMap(const char *key) const`**\
  Retrieves a CBOR map associated with a string key.

**Data Retrieval:**

* **`bool getBool(int key) const`**\
  Retrieves a boolean value associated with an integer key.

* **`bool getBool(const char *key) const`**\
  Retrieves a boolean value associated with a string key.

* **`long getInt(int key) const`**\
  Retrieves an integer value associated with an integer key.

* **`long getInt(const char *key) const`**\
  Retrieves an integer value associated with a string key.

* **`String getString(int key) const`**\
  Retrieves a string value associated with an integer key.

* **`String getString(const char *key) const`**\
  Retrieves a string value associated with a string key.

* **`String getValueAsString(int key) const`**\
  Retrieves the value as a string, regardless of its original type, associated with an integer key.

* **`String getValueAsString(const char *key) const`**\
  Retrieves the value as a string, regardless of its original type, associated with a string key.

* **`Bytes getBytes(int key) const`**\
  Retrieves a byte array associated with an integer key.

* **`Bytes getBytes(const char *key) const`**\
  Retrieves a byte array associated with a string key.

**Serialization and Deserialization:**

* **`Bytes build() const`**\
  Serializes the internal CBOR structure into a byte array for storage or transmission.

* **`void read(const Bytes &buf)`**\
  Deserializes the provided byte buffer and populates the CBOR object with the decoded data.

**State Management:**

* **`bool dirty() const`**\
  Checks if the CBOR object has been modified since the last store operation.

* **`void forceDirty()`**\
  Forces the CBOR object to be marked as dirty.

* **`void clean()`**\
  Resets the CBOR object to its initial state.

**Error Handling:**

* **`cn_cbor_errback getLastError()`**\
  Retrieves the last error encountered during CBOR operations.

## Inner Classes

### Array

The `Array` class is a nested class within `CBORObject` that facilitates the manipulation of CBOR arrays. It provides methods to append various data types to the array and to create nested arrays, enabling the construction of complex data structures.

**Constructor and Destructor:**

* **`Array(CBORObject *context, cn_cbor *arrayNode)`**\
  Constructs an `Array` instance with a given context and CBOR array node.

    * **`context`** (`CBORObject *`): Pointer to the parent `CBORObject`.
    * **`arrayNode`** (`cn_cbor *`): Pointer to the CBOR array node.

* **`Array(const Array &other)`**\
  Copy constructor.

* **`Array &operator=(const Array &other)`**\
  Copy assignment operator.

* **`~Array()`**\
  Destructor that cleans up the array instance.

**Methods:**

* **`Array &append(int value)`**\
  Appends an integer value to the array.

* **`Array &append(const char *value)`**\
  Appends a string value to the array.

* **`template <typename T> Array &append(size_t size, const T *value)`**\
  Appends a sequence of integral values to the array.

* **`Array appendArray()`**\
  Appends a new nested array to the current array and returns it.

* **`cn_cbor_errback getLastError()`**\
  Retrieves the last error encountered during array operations.

**Private Methods:**

* **`void _create()`**\
  Initializes the internal CBOR structure for the [`COSEMessage`](cosemessage.md).

* **`bool _read(const Bytes &buf)`**\
  Parses a byte buffer to populate the `COSEMessage`.

* **`void _clean()`**\
  Cleans up the internal CBOR structure and resets pointers.

* **`bool _setProtectedHeader(const CBORObject &pHeader)`**\
  Sets the protected header in the `COSEMessage`.

* **`bool _setSignature(const Bytes &signature)`**\
  Sets the signature in the `COSEMessage`.

* **`Bytes _toBeSigned(const Bytes &external = Bytes())`**\
  Constructs the byte sequence to be signed for message authentication.

* **`CBORObject _getMap(cn_cbor *cb)`**\
  Retrieves a CBOR map from a given CBOR node.

* **`long _getBool(cn_cbor *cb) const`**\
  Retrieves a boolean value from a CBOR node.

* **`long _getInt(cn_cbor *cb) const`**\
  Retrieves an integer value from a CBOR node.

* **`String _getString(cn_cbor *cb) const`**\
  Retrieves a string value from a CBOR node.

* **`Bytes _getBytes(cn_cbor *cb) const`**\
  Retrieves a byte array from a CBOR node.

* **`String _getValueAsString(cn_cbor *cb) const`**\
  Retrieves the value of a CBOR node as a string, regardless of its original type.

* **`bool _isPtrEqual(cn_cbor *cb, const void *ptr) const`**\
  Checks if a pointer is equal to the data pointer of a CBOR node.

* **`void _markAsDirty(bool updated)`**\
  Marks the CBOR object as dirty if an update has occurred.

* **`cn_cbor_errback *_errback()`**\
  Retrieves a pointer to the current error state, resetting it afterward.

**Type Definitions:**

* **`using SchedulerTaskCallback = std::function<void(SchedulerTask &, short)>`**\
  Type alias for a callback function that takes a reference to a [`SchedulerTask`](../scheduler/schedulertask.md) and a `short` indicating remaining executions.

* **`using spSchedulerTaskCallback = SharedPointer<SchedulerTaskCallback>`**\
  Type alias for a shared pointer to a `SchedulerTaskCallback`.
