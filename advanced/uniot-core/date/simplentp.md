# SimpleNTP

The `SimpleNTP` class manages the communication with NTP servers to obtain accurate epoch times. It handles the construction and parsing of NTP packets, manages retries and timeouts, and integrates with the [`Date`](date.md) class through callback mechanisms.

**Methods:**

* **`SimpleNTP()`**\
Constructs a `SimpleNTP` instance, initializing callback pointers.

* **`void setSyncTimeCallback(SyncTimeCallback callback)`**\
Sets the callback function to be invoked upon successful NTP synchronization.

* **`time_t getNtpTime()`**\
Initiates the process of retrieving the current epoch time from NTP servers.

**Private Methods:**

* **`bool _sendNTPPacket(WiFiUDP &udp)`**\
Constructs and sends an NTP request packet to a randomly selected NTP server from the predefined list.

* **`bool _waitForResponse(WiFiUDP &udp, unsigned long timeout, int maxRetries, unsigned long retryDelay)`**\
Waits for a response from the NTP server within the specified timeout and number of retries.

* **`time_t _processNTPResponse(WiFiUDP &udp)`**\
Processes the received NTP response packet to extract the epoch time.

**Private Members:**

* **`SyncTimeCallback mSyncTimeCallback`**\
Function pointer to the callback function invoked upon successful time synchronization.
