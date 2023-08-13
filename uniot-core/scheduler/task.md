---
description: Scheduling and Management of Timed Callbacks
---

# Task

The `Task` class allows the scheduling of tasks that can be run once or repeatedly with a specified interval in the Uniot project. It wraps the low-level timer functionality provided by the ESP8266 SDK and allows for efficient task management. Its design ensures that developers can quickly attach or detach tasks and build flexible scheduling mechanisms. By using templates, it also supports tasks with different types of arguments, adding to its versatility within the Uniot Core framework.

**Constructor and Destructor**:

* **`Task()`**: Constructor that initializes an instance of the `Task` class without any associated timer.
* **`virtual ~Task()`**: Destructor that ensures proper cleanup of the timer if it was attached.

**Task Scheduling:**

* **`void attach(uint32_t ms, bool repeat, TaskCallback callback)`**:
  * **`ms`**: Duration in milliseconds after which the callback should be executed.
  * **`repeat`**: Boolean flag. If `true`, the callback will be repeated at regular intervals defined by `ms`.
  * **`callback`**: Function pointer to the callback with signature **`void foo()`**.
  * Schedules a callback to be executed after a given duration. If `repeat` is `true`, the callback will be executed at regular intervals.
* **`void attach(uint32_t ms, bool repeat, TaskTypeCallback<T> callback, T arg)`**:
  * **`ms`**, **`repeat`**: Same as above.
  * **`callback`**: Function pointer to the callback with signature **`void foo(T arg)`**.
  * **`arg`**: Argument of type `T` to be passed to the callback.
  * Schedules a callback with an argument to be executed after a specified duration. **Note:** the size of the argument `T` must be less than or equal to 4 bytes.
* **`void detach()`**: Stops the task if it's running and deallocates any associated resources.

**Status Check:**

* **`bool isAttached()`**: Returns whether the task is currently attached.

**Internal Logic:**

* **`void attach_arg(uint32_t ms, bool repeat, TaskArgCallback callback, uint32_t arg)`**: A private method that handles the common logic for task attachment. It disarms the timer if it's already set, allocates a new timer if needed, sets the timer function and argument, and then arms the timer with the specified interval and repeat flag.

**Private Members:**

* **`ETSTimer *mpTimer`**: A pointer to an `ETSTimer` object that represents the underlying timer used to schedule callbacks.

**Type Definitions:**

* **`using TaskCallback = void (*)(void)`**: Type definition for a task callback with no arguments.
* **`using TaskArgCallback = void (*)(void *)`**: Type definition for a task callback with a single void pointer argument.
* **`template <typename T> using TaskTypeCallback = void (*)(T)`**: Template type definition for a task callback with a single argument of type `T`.
