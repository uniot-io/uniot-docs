---
description: Scheduling Individual Tasks
---

# SchedulerTask

The `SchedulerTask` class is a specialization of the [`Task`](task.md) class, enabling controlled execution of repetitive or one-time tasks within the Uniot Core's scheduling system. It provides mechanisms to schedule tasks at specific intervals and manage their execution states effectively.

**Constructors:**

* **`SchedulerTask(IExecutor &executor)`**\
  Constructs a `SchedulerTask` by taking an [`IExecutor`](iexecutor.md) instance. This constructor initializes the task to execute the provided executor's logic when triggered. It internally sets up a callback that calls the `execute` method of the given `IExecutor` instance with the remaining number of repetitions.

* **`SchedulerTask(SchedulerTaskCallback callback)`**\
  Constructs a `SchedulerTask` with a specified callback function. The callback is a `std::function` that defines the task's behavior and is invoked each time the task is executed. This allows for flexible and customizable task actions.

**Methods:**

* **`void attach(uint32_t ms, short times = 0)`**\
  Attaches the task to the scheduler with a specified interval and repetition count.

  * **`ms`**: Duration in milliseconds between each execution of the task.
  * **`times`**: Number of times the task should repeat. If set to `0`, the task repeats indefinitely.

* **`void once(uint32_t ms)`**\
  Schedules the task to execute once after a specified delay.

* **`void loop()`**\
  Executes the task if it is due for execution.

* **`uint64_t getTotalElapsedMs() const`**\
  Retrieves the total elapsed time since the task was scheduled.

**Private Members:**

* **`uint64_t mTotalElapsedMs`**\
  Tracks the total elapsed time in milliseconds since the `SchedulerTask` was instantiated. This provides a global time reference for the task's execution lifecycle.

* **`short mRepeatTimes`**\
  Indicates the number of remaining times the task should execute. A positive value specifies the exact number of repetitions, while a value of `-1` signifies infinite repetitions.

* **`volatile bool mCanDoHardWork`**\
  A flag that indicates whether the task is ready to perform its operation. This flag is set by the timer callback and checked during each loop iteration to determine if the task should be executed.

* **`spSchedulerTaskCallback mspCallback`**\
  A shared pointer to the task's callback function. This callback defines the specific actions the task performs upon execution. Using a shared pointer ensures proper memory management and allows for flexible callback definitions.

**Type Definitions:**

* **`using SchedulerTaskCallback = std::function<void(SchedulerTask &, short)>`**\
  A type alias for a callback function that takes a reference to the `SchedulerTask` and a `short` indicating the remaining number of repetitions. This callback is invoked each time the task is executed, allowing for dynamic task behavior based on the remaining executions.

* **`using spSchedulerTaskCallback = SharedPointer<SchedulerTaskCallback>`**\
  A type alias for a shared pointer to a `SchedulerTaskCallback`. This ensures that the callback function is properly managed and can be shared across different parts of the system without risking memory leaks.
