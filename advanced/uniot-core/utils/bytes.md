# Bytes

The **Bytes** utility provides a versatile and efficient means of handling byte arrays, facilitating operations such as serialization, deserialization, memory management, and data manipulation.

**Key Features:**
- Dynamic memory management with automatic allocation and deallocation.
- Support for various data sources, including C-style arrays, strings, and integral types.
- Utility functions for hexadecimal conversions, checksum calculations, and data termination.
- Memory safety with bounds checking and error handling.
- Integration with other Uniot components through seamless data handling.

**Constructors and Destructor:**

* **`Bytes()`**\
Constructs an empty Bytes instance with no allocated memory.

* **`Bytes(const uint8_t *data, size_t size)`**\
Constructs a Bytes instance by copying data from a given byte buffer.

* **`Bytes(const char *str)`**\
Constructs a Bytes instance from a C-style null-terminated string. It automatically includes the null terminator in the byte array.

* **`template <typename T> Bytes(T value)`**\
Constructs a Bytes instance from an integral type. This enables easy conversion of numerical values to byte arrays.

* **`Bytes(const Bytes &value)`**\
Copy constructor that creates a new Bytes instance by copying another Bytes instance.

* **`Bytes(const String &value)`**\
Constructs a Bytes instance from a String object. It copies the string data into the byte array.

* **`virtual ~Bytes()`**\
Destructor that deallocates the memory used by the Bytes instance, preventing memory leaks.

**Assignment Operators:**

* **`Bytes &operator=(const Bytes &rhs)`**\
Copy assignment operator that assigns the contents of one Bytes instance to another.

* **`Bytes &operator=(const String &rhs)`**\
Assigns a String object to a Bytes instance, copying the string data into the byte array and ensuring null termination.

**Static Methods:**

* **`static Bytes fromHexString(const String &hexStr)`**\
Creates a Bytes instance from a hexadecimal string representation. Each pair of hexadecimal characters is converted to a single byte.

  > Notes:
  > - The input string must have an even length; otherwise, the function logs an error and returns an empty `Bytes` instance.
  > - The function uses strtol for hexadecimal conversion, ensuring accurate byte representation.

**Utility Methods:**

* **`size_t fill(Filler filler)`**\
Fills the byte array using a user-provided filler function. The filler function defines how the buffer should be populated.

  * filler (Filler): A std::function that takes a pointer to the buffer and its size, and returns the number of bytes written.
  * Returns the number of bytes successfully written by the filler function.

* **`Bytes &prune(size_t newSize)`**\
Reduces the size of the byte array to newSize bytes if newSize is smaller than the current size. This helps in trimming excess memory usage.

* **`const uint8_t *raw() const`**\
Provides a const pointer to the underlying byte buffer, allowing read-only access to the data.

* **`Bytes &terminate()`**\
Ensures that the byte array is null-terminated. If the last byte is not '\0', it appends a null terminator by reallocating the buffer.

* **`const char *c_str() const`**\
Provides a C-style null-terminated string representation of the byte array. Returns const pointer to the first character of the buffer.

* **`String toString() const`**\
Converts the byte array to an Arduino String object. This is useful for interfacing with APIs that require String types.

* **`String toHexString() const`**\
Converts the byte array to its hexadecimal string representation. Each byte is represented by two hexadecimal characters.

* **`size_t size() const`**\
Retrieves the current size of the byte array in bytes.

* **`void clean()`**\
Clears the byte array by deallocating the memory and resetting the size to zero.

* **`uint32_t checksum() const`**\
Calculates a CRC32 checksum of the byte array, useful for data integrity verification.

**Private Helper Methods:**

* **`inline void _init(void)`**\
Initializes the internal state of the `Bytes` instance by setting the buffer pointer to `nullptr` and size to zero.

* **`void _invalidate(void)`**\
Frees the allocated memory buffer and resets the internal state to prevent memory leaks and dangling pointers.

* **`bool _reserve(size_t newSize)`**\
Reserves memory for the byte array by reallocating the buffer to the specified `newSize`.

* **`Bytes &_copy(const uint8_t *data, size_t size)`**\
Copies data from a source byte buffer into the `Bytes` instance after reserving the necessary memory.

**Private Members:**

* **`uint8_t *mBuffer`**\
Pointer to the dynamically allocated byte buffer.

* **`size_t mSize`**\
Current size of the byte array in bytes.
