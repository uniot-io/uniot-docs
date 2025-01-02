# CrashStorage

The `CrashStorage` class extends the [`Storage`](storage.md) class to log crash information specifically for the ESP8266 platform. It captures reset information and stack traces to aid in debugging and post-mortem analysis.

**Constructor and Destructor:**

* **`CrashStorage(const String &path)`**\
  Constructs a `CrashStorage` instance with a specified file path.

* **`virtual ~CrashStorage()`**\
  Destructor that ensures proper cleanup.

**Methods:**

* **`bool store() override`**\
  Stores the crash data to the specified file.

* **`bool clean() override`**\
  Cleans the crash data by resetting crash information and removing the file.

* **`bool printCrashDataIfExists() const`**\
  Prints the crash data to the serial console if it exists.

**Protected Members:**

* **`CBORObject mCbor`** (inherited from `Storage` via `CBORStorage`):
  Manages structured CBOR data for crash information.

* **`struct rst_info *mResetInfo`**\
  Pointer to the reset information structure containing details about the crash.

* **`uint32_t mStackStart`**\
  Starting address of the stack trace.

* **`uint32_t mStackEnd`**\
  Ending address of the stack trace.

**Private Members:**

* **`void setCrashInfo(struct rst_info* resetInfo, uint32_t stackStart, uint32_t stackEnd)`**\
  Sets the crash information for logging.

  * **`resetInfo`** (`struct rst_info*`): Pointer to the reset information structure.
  * **`stackStart`** (`uint32_t`): Starting address of the stack trace.
  * **`stackEnd`** (`uint32_t`): Ending address of the stack trace.

* **`Bytes buildDumpData() const`**\
  Constructs the crash dump data from the reset information and stack trace.
