---
description: Central Scheduler for Managing Tasks
---

# TaskScheduler

The `TaskScheduler` class is the cornerstone of time management within the Uniot Core. It is responsible for scheduling, executing, and managing multiple tasks, ensuring that each task runs at its designated interval. By maintaining an organized queue of tasks, `TaskScheduler` plays a vital role in the overall functionality and efficiency of the system.

**Static Factory Methods:**

* **`static TaskPtr make(SchedulerTask::SchedulerTaskCallback callback)`**\
  Creates a shared pointer to a [`SchedulerTask`](schedulertask.md) with a specified callback function. This allows tasks to execute custom logic defined by the provided callback.

* **`static TaskPtr make(IExecutor &executor)`**\
  Creates a shared pointer to a `SchedulerTask` using an [`IExecutor`](iexecutor.md) instance. This enables tasks to execute predefined executor logic.

**Constructor:**

* **`TaskScheduler()`**\
  Initializes a new instance of the `TaskScheduler` class, setting the total elapsed milliseconds to zero.

**Task Management:**

* **`TaskScheduler &push(const char *name, TaskPtr task)`**\
  Adds a `SchedulerTask` to the scheduler's queue for execution with an associated name. The name can be used for identification and management purposes.

* **`TaskScheduler &push(ISchedulerConnectionKit &connection)`**\
  Enables the scheduler to add tasks via the [`ISchedulerConnectionKit`](ischedulerconnectionkit.md) interface, providing flexibility in task sources. This allows external components to integrate their tasks seamlessly into the scheduler.

* **`void loop()`**\
  Iterates through all scheduled tasks, invoking their respective `loop` methods to execute any due tasks. This method should be called regularly, typically within the main loop of the firmware, to ensure timely task execution.

* **`void exportTasksInfo(TaskInfoCallback callback) const`**\
  Exports information about all scheduled tasks by invoking the provided callback for each task. The callback receives the task's name, its attachment status, and the total elapsed milliseconds since it was scheduled. This is useful for debugging, monitoring, or displaying task statuses.

* **`uint64_t getTotalElapsedMs() const`**\
  Retrieves the total elapsed milliseconds since the scheduler started. This can be used for performance monitoring or timing-related functionalities within the system.

**Private Members:**

* **`uint64_t mTotalElapsedMs`**\
  Tracks the total elapsed time in milliseconds since the `TaskScheduler` was instantiated. This provides a global time reference for all tasks managed by the scheduler.

* **`ClearQueue<Pair<const char *, TaskPtr>> mTasks`**\
  A queue that stores pairs of task names and their corresponding task pointers. This structure allows the scheduler to manage multiple tasks efficiently, ensuring that each task is executed according to its schedule.

**Type Definitions:**

* **`using TaskPtr = SharedPointer<SchedulerTask>`**\
  A type alias for a shared pointer to a `SchedulerTask`. This is used within the `TaskScheduler` class for managing individual task objects, ensuring proper memory management and ownership semantics.

* **`using TaskInfoCallback = std::function<void(const char *, bool, uint64_t)>`**\
  A type alias for a callback function used in `exportTasksInfo`. The callback receives the task's name (`const char *`), its attachment status (`bool`), and the total elapsed milliseconds (`uint64_t`).
