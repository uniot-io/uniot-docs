---
description: Bridge for Efficient Integration of Components
---

# ISchedulerConnectionKit

`ISchedulerConnectionKit` is an interface that provides a contract for objects that need to connect with a `TaskScheduler`. Implementing this interface allows a class to define how it should push tasks to a scheduler and how to attach itself. This creates a standardized way for objects to interact with the task scheduling system, enhancing modularity and maintainability of the codebase.

**Destructor:**

* **`virtual ~ISchedulerConnectionKit()`**\
  A virtual destructor ensures that the destructor of any derived classes is called correctly when an object is deleted through a pointer to this interface. This is crucial for proper resource cleanup and avoiding memory leaks.

**Methods:**

* **`virtual void pushTo(TaskScheduler &scheduler) = 0`**\
  A pure virtual method that requires any class implementing this interface to define how it interacts with the `TaskScheduler`. This method is responsible for adding one or more tasks to the scheduler. The exact implementation can vary depending on the specific needs of the derived class, such as adding different types of tasks or configuring task parameters.

* **`virtual void attach() = 0`**\
  Another pure virtual method that requires implementing classes to define their behavior upon attachment. This method is intended for initializing or setting up any necessary components before the tasks are scheduled and executed.
