---
description: Scheduling Individual Tasks
---

# SchedulerTask

The `SchedulerTask` class is a specialization of a `Task` that enables more controlled execution of repetitive or one-time tasks. It implements the `IExecutor` interface, allowing it to be used with the Uniot Core's main time management system.

**Constructors:**

* **`SchedulerTask(IExecutor *executor)`**: Constructor that takes another `IExecutor` and executes it within the task.
* **`SchedulerTask(SchedulerTaskCallback callback)`**: Constructor that takes a specific callback function with signature **`void foo(short)`** to be executed within the task.

**Methods:**

* **`void attach(uint32_t ms, short times = 0)`**:
  * **`ms`**: Duration in milliseconds for the task to execute.
  * **`times`**: Number of times the task should repeat. Defaults to 0 for indefinite repetition.
  * Attaches the task to the scheduler for execution.
* **`virtual uint8_t execute() override`**: Implements the `IExecutor` interface, executing the task based on the scheduling logic.

**Private Members:**

* **`short mRepeatTimes`**: Number of times the task should repeat.
* **`volatile bool mCanDoHardWork`**: A flag indicating whether the task can perform its operation.
* **`spSchedulerTaskCallback mspCallback`**: Shared pointer to the task's callback function.

**Type Definitions:**

* **`using SchedulerTaskCallback = std::function<void(short)>`**: Type alias for a standard function that takes a short integer as a parameter. This callback is used to define the task's behavior within the `SchedulerTask` class.
* **`using spSchedulerTaskCallback = SharedPointer<SchedulerTaskCallback>`**: Type alias for a shared pointer to a `SchedulerTaskCallback`. Utilized within the `SchedulerTask` class for managing the task's callback.
