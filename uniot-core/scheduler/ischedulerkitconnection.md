---
description: Bridge for Efficient Integration of Components
---

# ISchedulerKitConnection

`ISchedulerKitConnection` is an interface that provides a contract for objects that need to connect with a `TaskScheduler`. Implementing this interface allows a class to define how it should push tasks to a scheduler and how to attach itself. This creates a standard way for objects to interact with the task scheduling system, making the code more modular and easier to maintain.

**Destructor:**

* **`virtual ~ISchedulerKitConnection()`**: A virtual destructor ensures that the destructor of any derived classes is called correctly when an object is deleted through a pointer to this interface.

**Methods:**

* **`virtual void pushTo(TaskScheduler *scheduler) = 0`**: A pure virtual method which requires any class implementing this interface to define how it gets pushed into the `TaskScheduler`. This could mean adding one or more tasks to the scheduler, or some other form of interaction to ensure that the object's operations are accounted for in the broader scheduling system. The precise nature of "pushing" will depend on the needs of the derived class.
* **`virtual void attach() = 0`**: Another pure virtual method, demanding the implementing classes to define their behavior when "attached." This could represent the initialization of a task, device, or other operations which need to be executed before the object starts its scheduled operations within the Uniot Core system.
