# NetworkScheduler

The `NetworkScheduler` class oversees network-related tasks, including initiating WiFi connections, managing a captive portal for network setup, and monitoring the network status. It interacts with the [`TaskScheduler`](../scheduler/taskscheduler.md) to schedule and execute tasks that handle various network states, ensuring that the device can connect to available networks, fallback to an access point mode when necessary, and recover from connection failures gracefully.

**Constructor:**

* **`NetworkScheduler(Credentials &credentials)`**\
  Initializes the network scheduler by setting up the access point name, configuring WiFi settings, and initializing network-related tasks. It disables persistent WiFi storage to prevent unexpected behaviors and sets the WiFi mode to station (`WIFI_STA`). The constructor also initializes server callbacks for the captive portal and prepares tasks for managing network connections.

**Methods:**

* **`void pushTo(TaskScheduler &scheduler) override`**\
  Pushes all network-related tasks to the provided [`TaskScheduler`](../scheduler/taskscheduler.md). Adds tasks such as server start, server serve, server stop, access point configuration, station connection, connecting status, and WiFi monitoring to the scheduler for execution.

* **`void attach() override`**\
  Attaches network tasks based on stored credentials.

* **`void forget()`**\
  Clears stored WiFi credentials and initiates access point configuration.

* **`bool reconnect()`**\
  Attempts to reconnect to the WiFi network using stored credentials.

**Private Members:**

* **`Credentials *mpCredentials`**\
  Pointer to the associated [`Credentials`](../credentials.md) instance containing WiFi credentials.

* **`WifiStorage mWifiStorage`**\
  Instance of `WifiStorage` for managing persistent WiFi credentials storage.

* **`String mApName`**\
  Name of the access point (AP) created for the captive portal. Formatted as `"UNIOT-"` followed by the device's short ID in hexadecimal.

* **`IPAddress mApSubnet`**\
  Subnet mask for the access point. Set to `255.255.255.0`.

* **`ConfigCaptivePortal mConfigServer`**\
  Instance of [`ConfigCaptivePortal`](configcaptiveportal.md) managing the captive portal web server for network configuration.

* **`TaskScheduler::TaskPtr mTaskStart`**\
  Task pointer for starting the captive portal server.

* **`TaskScheduler::TaskPtr mTaskServe`**\
  Task pointer for handling client requests to the captive portal server.

* **`TaskScheduler::TaskPtr mTaskStop`**\
  Task pointer for stopping the captive portal server.

* **`TaskScheduler::TaskPtr mTaskConfigAp`**\
  Task pointer for configuring the access point settings.

* **`TaskScheduler::TaskPtr mTaskConnectSta`**\
  Task pointer for initiating a WiFi station connection.

* **`TaskScheduler::TaskPtr mTaskConnecting`**\
  Task pointer for monitoring the WiFi connection status during the connecting phase.

* **`TaskScheduler::TaskPtr mTaskMonitoring`**\
  Task pointer for monitoring the ongoing WiFi connection status.

### Private Methods

* **`void _initTasks()`**\
  Sets up tasks for starting and stopping the captive portal server, configuring the access point, initiating station connections, monitoring connection status, and handling connection retries. Each task is associated with a lambda function that defines its specific behavior.

* **`void _initServerCallbacks()`**\
  Sets up HTTP request handlers for the captive portal web server.

**Type Definitions:**

* **`enum Channel { OUT_SSID = FOURCC(ssid) }`**\
  Enumeration defining channels for emitting network-related data, such as the SSID of the connected network.

* **`enum Topic { CONNECTION = FOURCC(netw) }`**\
  Enumeration defining event topics related to network connection statuses.

* **`enum Msg { FAILED = 0, SUCCESS, CONNECTING, DISCONNECTED, ACCESS_POINT }`**\
  Enumeration defining messages representing various network connection states.
