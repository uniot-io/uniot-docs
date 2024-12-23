# NetworkController

The `NetworkController` class manages network configurations, user interactions through buttons, and status indicators using LEDs. It integrates with the [`NetworkScheduler`](networkscheduler.md) to handle connection events, manage reboot logic based on connection stability, and ensure that the device maintains a reliable network connection. The controller also handles user-initiated actions such as reconnecting to the network or resetting network configurations.

**Constructor and Destructor:**

* **`NetworkController(NetworkScheduler &network, uint8_t pinBtn = UINT8_MAX, uint8_t activeLevelBtn = LOW, uint8_t pinLed = UINT8_MAX, uint8_t activeLevelLed = HIGH, uint8_t maxRebootCount = 3, uint32_t rebootWindowMs = 10000)`**\
  Initializes the `NetworkController`, setting up the LED and button if specified. It initializes tasks for LED signaling, button configuration, and reboot count management. The constructor also restores any saved reboot counts and starts monitoring for reboot conditions. Additionally, it listens to network connection events to update the system status accordingly.

  * **`network`** (`NetworkScheduler &`): Reference to the `NetworkScheduler` instance for managing network tasks.
  * **`pinBtn`** (`uint8_t`): GPIO pin number for the configuration button. Defaults to `UINT8_MAX` if no button is used.
  * **`activeLevelBtn`** (`uint8_t`): Active logic level for the button (`HIGH` or `LOW`). Defaults to `LOW`.
  * **`pinLed`** (`uint8_t`): GPIO pin number for the status LED. Defaults to `UINT8_MAX` if no LED is used.
  * **`activeLevelLed`** (`uint8_t`): Active logic level for the LED (`HIGH` or `LOW`). Defaults to `HIGH`.
  * **`maxRebootCount`** (`uint8_t`): Maximum number of reboots allowed within the reboot window. Defaults to `3`.
  * **`rebootWindowMs`** (`uint32_t`): Time window in milliseconds to monitor reboot counts. Defaults to `10000` ms.

* **`virtual ~NetworkController()`**\
  Destructor that ensures proper cleanup by stopping event listening and releasing network scheduler references.

**Methods:**

* **`bool store() override`**\
  Stores the current reboot count to persistent storage.

* **`bool restore() override`**\
  Restores the reboot count from persistent storage.

* **`void onEventReceived(unsigned int topic, int msg) override`**\
  Handles network connection events such as `ACCESS_POINT`, `SUCCESS`, `CONNECTING`, `DISCONNECTED`, and `FAILED`. Based on the event, it updates the LED status and manages reconnection attempts or resets the network configuration as needed.

* **`void pushTo(TaskScheduler &scheduler) override`**\
  Pushes the controller's tasks to the provided [`TaskScheduler`](../scheduler/taskscheduler.md).

* **`void attach() override`**\
  Attaches the controller's tasks to the scheduler and initializes the system status.

* **`void statusWaiting()`**\
  Updates the LED to indicate a waiting status.

* **`void statusBusy()`**\
  Updates the LED to indicate a busy status.

* **`void statusAlarm()`**\
  Updates the LED to indicate an alarm or error status.

* **`void statusIdle()`**\
  Updates the LED to indicate an idle status.

* **`Button* getButton()`**\
  Retrieves the configuration button instance if available.

**Private Members:**

* **`NetworkScheduler *mpNetwork`**\
  Pointer to the associated `NetworkScheduler` instance responsible for managing network tasks.

* **`int mNetworkLastState`**\
  Stores the last known network state to track changes and handle reconnections appropriately.

* **`uint8_t mClickCounter`**\
  Counts the number of button clicks within a specific time window to handle multi-click actions.

* **`uint8_t mPinLed`**\
  GPIO pin number assigned to the status LED. If set to `UINT8_MAX`, no LED is used.

* **`uint8_t mActiveLevelLed`**\
  Active logic level for the LED (`HIGH` or `LOW`), determining how the LED is controlled.

* **`uint8_t mMaxRebootCount`**\
  Maximum number of allowed reboots within the reboot window before triggering a network forget/reset.

* **`uint32_t mRebootWindowMs`**\
  Time window in milliseconds to monitor the number of reboots.

* **`uint8_t mRebootCount`**\
  Current count of reboots that have occurred within the specified reboot window.

* **`UniquePointer<Button> mpConfigBtn`**\
  Unique pointer to the configuration `Button` instance. Manages button interactions for network configuration.

* **`TaskScheduler::TaskPtr mpTaskSignalLed`**\
  Task pointer for managing LED signaling based on network status.

* **`TaskScheduler::TaskPtr mpTaskConfigBtn`**\
  Task pointer for handling button configuration actions.

* **`TaskScheduler::TaskPtr mpTaskResetClickCounter`**\
  Task pointer for resetting the button click counter after a specified duration.

* **`TaskScheduler::TaskPtr mpTaskResetRebootCounter`**\
  Task pointer for resetting the reboot count after the reboot window duration.

**Type Definitions:**

* **`enum Topic { NETWORK_LED = FOURCC(nled) }`**\
  Enumeration defining event topics related to network LED signaling.
