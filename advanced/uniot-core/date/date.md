# Date

The `Date` class provides functionalities to synchronize system time with NTP servers, retrieve the current time, and manage time-related events. It ensures that the system maintains accurate time, which is essential for various operations such as logging, scheduling, and data timestamping.

**Constructor:**

* **`Date()`**\
Private constructor, initializes the `Date` instance, sets up NTP callbacks, configures NTP servers, and restores stored time.

**Methods:**

* **`static time_t now()`**\
Retrieves the current epoch time.

* **`static String getFormattedTime()`**\
Returns the current time as a formatted string (e.g., "YYYY-MM-DD HH:MM:SS").

* **`bool store() override`**\
Stores the current epoch time into persistent CBOR storage.

* **`bool restore() override`**\
Restores the epoch time from CBOR storage and sets the system time accordingly.

* **`void execute(short _) override`**\
Executes the store operation, typically called after successful time synchronization to persist the updated epoch time.

* **`void forceSync()`**\
Forces a synchronization with NTP servers to update the system time immediately, bypassing scheduled synchronization intervals.

**Private Methods:**

* **`void _timeSyncCallback()`**\
Callback function invoked upon successful time synchronization. Executes the store operation and emits a synchronization event.

* **`bool _setTime(time_t epoch)`**\
Sets the system time to the specified epoch value.

* **`void _reconfigure()`**\
Configures the NTP settings by specifying the NTP servers to use for time synchronization.

* **`time_t _now()`**\
Retrieves the current system epoch time.

* **`String _getFormattedTime()`**\
Generates a formatted time string based on the current system time.

**Private Members:**

* **`SimpleNTP mSNTP`**\
Instance of the `SimpleNTP` class responsible for handling NTP communications and time synchronization.
