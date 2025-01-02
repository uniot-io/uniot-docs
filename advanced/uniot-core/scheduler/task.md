---
description: Scheduling and Management of Timed Callbacks
---

# Task

The `Task` class enables the scheduling of tasks that can be run once or repeatedly at specified intervals. It abstracts the low-level timer functionalities provided by different ESP SDKs, allowing for efficient and flexible task management. The design supports tasks with and without arguments, enhancing its versatility within the Uniot Core.

## ESP8266Task

The `ESP8266Task` class is a specialization of the `Task` class tailored for the ESP8266 platform. It leverages the ESP8266 SDK's timer functions to manage task scheduling and execution.

**Constructor and Destructor:**

* **`ESP8266Task()`**\
  Constructor that initializes an instance of the `ESP8266Task` class without any associated timer. It sets the internal timer pointer to `nullptr`, indicating that no timer is currently attached.

* **`virtual ~ESP8266Task()`**\
  Destructor that ensures proper cleanup of the timer if it was attached. It calls the `detach()` method to disarm and delete the timer, preventing memory leaks and ensuring that resources are freed appropriately.

**Task Scheduling:**

* **`void attach(uint32_t ms, bool repeat, TaskCallback callback)`**\
  Schedules a callback to be executed after a given duration.
  * **`ms`**: Duration in milliseconds after which the callback should be executed.
  * **`repeat`**: Boolean flag. If `true`, the callback will be repeated at regular intervals defined by `ms`.
  * **`callback`**: Function pointer to the callback with signature **`void foo()`**.

* **`template <typename T> void attach(uint32_t ms, bool repeat, TaskTypeCallback<volatile T> callback, volatile T arg)`**\
  Schedules a callback with an argument to be executed after a specified duration. **Note:** The size of the argument `T` must be less than or equal to 4 bytes to ensure proper handling within the ESP8266's memory constraints.
  * **`ms`**, **`repeat`**: Same as above.
  * **`callback`**: Function pointer to the callback with signature **`void foo(volatile T arg)`**.
  * **`arg`**: Argument of type `T` to be passed to the callback.

* **`void detach()`**\
  Stops the task if it's running and deallocates any associated resources. It disarms the timer and deletes the `ETSTimer` object to prevent resource leaks.

**Status Check:**

* **`bool isAttached()`**\
  Returns whether the task is currently attached.

**Internal Logic:**

* **`void attach_arg(uint32_t ms, bool repeat, TaskArgCallback callback, volatile void *arg)`**\
  A private method that handles the common logic for task attachment. It disarms the timer if it's already set, allocates a new timer if needed, sets the timer function and argument, and then arms the timer with the specified interval and repeat flag. This method ensures that tasks are attached consistently, regardless of whether they have arguments.

**Private Members:**

* **`ETSTimer *mpTimer`**\
  A pointer to an `ETSTimer` object that represents the underlying timer used to schedule callbacks. It is initialized to `nullptr` and managed internally to handle task scheduling and execution.

**Type Definitions:**

* **`using TaskCallback = void (*)(void)`**\
  Type definition for a task callback with no arguments. This callback is used for tasks that do not require any external data when executed.

* **`using TaskArgCallback = void (*)(void *)`**\
  Type definition for a task callback with a single void pointer argument. This allows passing arbitrary data to the callback function during execution.

* **`template <typename T> using TaskTypeCallback = void (*)(volatile T)`**\
  Template type definition for a task callback with a single argument of type `T`. This facilitates defining callbacks that require specific data types, enhancing the flexibility of task definitions.

## ESP32Task

The `ESP32Task` class is a specialization of the `Task` class designed for the ESP32 platform. It utilizes the ESP-IDF's `esp_timer` API to manage task scheduling and execution efficiently.

**Constructor and Destructor:**

* **`ESP32Task()`**\
  Constructor that initializes an instance of the `ESP32Task` class without any associated timer. It sets the internal timer handle to `nullptr`, indicating that no timer is currently attached.

* **`virtual ~ESP32Task()`**\
  Destructor that ensures proper cleanup of the timer if it was attached. It calls the `detach()` method to stop and delete the timer, preventing resource leaks and ensuring that resources are freed appropriately.

**Task Scheduling:**

* **`void attach(uint32_t ms, bool repeat, TaskCallback callback)`**\
  Schedules a callback to be executed after a given duration.
  * **`ms`**: Duration in milliseconds after which the callback should be executed.
  * **`repeat`**: Boolean flag. If `true`, the callback will be repeated at regular intervals defined by `ms`.
  * **`callback`**: Function pointer to the callback with signature **`void foo()`**.

* **`template <typename T> void attach(uint32_t ms, bool repeat, TaskTypeCallback<volatile T> callback, volatile T arg)`**\
  Schedules a callback with an argument to be executed after a specified duration.
  * **`ms`**, **`repeat`**: Same as above.
  * **`callback`**: Function pointer to the callback with signature **`void foo(volatile T arg)`**.
  * **`arg`**: Argument of type `T` to be passed to the callback.

* **`void detach()`**\
  Stops the task if it's running and deallocates any associated resources. It stops the timer and deletes the `esp_timer` handle to prevent resource leaks.

**Status Check:**

* **`bool isAttached()`**\
  Returns whether the task is currently attached.

**Internal Logic:**

* **`void attach_arg(uint32_t ms, bool repeat, TaskArgCallback callback, volatile void *arg)`**\
  A private method that handles the common logic for task attachment. It disarms the timer if it's already set, allocates a new timer if needed, sets the timer function and argument, and then arms the timer with the specified interval and repeat flag. This method ensures that tasks are attached consistently, regardless of whether they have arguments.

**Private Members:**

* **`esp_timer_handle_t mpTimer`**\
  A handle to an `esp_timer` object that represents the underlying timer used to schedule callbacks. It is initialized to `nullptr` and managed internally to handle task scheduling and execution.

**Type Definitions:**

* **`using TaskCallback = void (*)(void)`**\
  Type definition for a task callback with no arguments. This callback is used for tasks that do not require any external data when executed.

* **`using TaskArgCallback = void (*)(void *)`**\
  Type definition for a task callback with a single void pointer argument. This allows passing arbitrary data to the callback function during execution.

* **`template <typename T> using TaskTypeCallback = void (*)(volatile T)`**\
  Template type definition for a task callback with a single argument of type `T`. This facilitates defining callbacks that require specific data types, enhancing the flexibility of task definitions.
