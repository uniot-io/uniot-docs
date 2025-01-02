---
description: Execution Command Abstraction
---

# IExecutor

The `IExecutor` interface is a fundamental part of the Uniot Core's execution mechanism. It defines the contract for executing a specific task and is leveraged by various components within the framework to ensure a uniform way of task execution.

**Destructor:**

* **`virtual ~IExecutor()`**: Virtual destructor ensuring proper destruction of derived classes.

**Methods:**

* **`virtual uint8_t execute() = 0`**: The pure virtual method that must be implemented by any class inheriting from `IExecutor`. This method encapsulates the logic for executing a specific task.
