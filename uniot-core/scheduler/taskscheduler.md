---
description: Central Scheduler for Managing Tasks
---

# TaskScheduler

The `TaskScheduler` and `SchedulerTask` classes form the core of time management within the Uniot Core. They are central to scheduling, executing, and managing tasks, thereby playing a vital role in the overall functioning of the system.

The heartbeat of Uniot Core's time management, `TaskScheduler` manages and orchestrates the execution of multiple tasks. It maintains a queue of `SchedulerTask` objects and is responsible for their scheduled execution.

**Static Factory Methods:**

* **`static TaskPtr make(SchedulerTask::SchedulerTaskCallback callback)`**: Creates a shared pointer to a `SchedulerTask` with a given callback.
* **`static TaskPtr make(IExecutor *executor)`**: Creates a shared pointer to a `SchedulerTask` with a given executor.

**Task Management:**

* **`TaskScheduler *push(TaskPtr task)`**: Adds a `SchedulerTask` to the scheduler's queue for execution.
* **`TaskScheduler *push(ISchedulerKitConnection *connection)`**: Enables the scheduler to add tasks via the `ISchedulerKitConnection` interface, providing flexibility in task sources.
* **`virtual uint8_t execute() override`**: Implements the `IExecutor` interface. Executes all the tasks in the queue and returns the count of attached tasks.

**Private Members:**

* **`ClearQueue<TaskPtr> mTasks`**: A queue of scheduled tasks.

**Type Definitions:**

* **`using TaskPtr = SharedPointer<SchedulerTask>`**: Type alias for a shared pointer to a `SchedulerTask`. Used in the `TaskScheduler` class for managing individual task objects.
