# Storage

The `Storage` class serves as the foundational component for handling file system operations. It abstracts the low-level details of the file system, providing simple methods to store, restore, and clean data. This class is designed to work seamlessly with both ESP8266 and ESP32 platforms by leveraging the appropriate file system libraries (`SPIFFS` or `LittleFS`).

**Constructor and Destructor:**

* **`Storage(const String &path)`**\
  Constructs a `Storage` instance with a specified file path.

* **`virtual ~Storage()`**\
  Destructor that ensures proper cleanup of the file system.

**Methods:**

* **`virtual bool store()`**\
  Stores the current data to the specified file.

* **`virtual bool restore()`**\
  Restores data from the specified file.

* **`virtual bool clean()`**\
  Cleans the stored data by clearing the buffer and removing the file.

* **`void setPath(const String &path)`**\
  Sets the file path for storage.

**Protected Members:**

* **`Bytes mData`**\
  Buffer holding the data to be stored or restored.

* **`String mPath`**\
  File path where data is stored.

**Private Members:**

* **`Bytes _readSmallFile(File &file)`**\
  Reads the contents of a file into a `Bytes` buffer.

* **`static bool sMounted`**\
  Static flag indicating whether the file system is currently mounted.

* **`static unsigned int sInstancesCount`**\
  Static counter tracking the number of `Storage` instances. Used to determine when to unmount the file system.

**Type Definitions:**

* **`using TaskCallback = void (*)(void)`**\
  Type definition for a task callback with no arguments.

* **`using TaskArgCallback = void (*)(void *)`**\
  Type definition for a task callback with a single void pointer argument.

* **`template <typename T> using TaskTypeCallback = void (*)(volatile T)`**\
  Template type definition for a task callback with a single argument of type `T`.
