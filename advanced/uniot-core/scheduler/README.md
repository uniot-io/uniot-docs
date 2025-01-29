---
description: Uniot Core Time Management System
---

# Scheduler

The Scheduler module in Uniot Core is an essential component that provides a robust and versatile time management system for the entire framework. Through a set of classes and interfaces, the Scheduler system ensures that tasks, devices, and various other elements are organized and executed according to specific time frames and requirements. This scheduling capability is fundamental to a wide range of applications, from simple periodic tasks to complex device interactions.

### Components

[**TaskScheduler**](taskscheduler.md)

The heart of the time management system in Uniot Core. It manages, schedules, and oversees the execution of all tasks. By maintaining a queue of tasks and executing them based on their individual schedules, it ensures the efficient and orderly operation of the entire Uniot Core system. It can also push tasks and interact with various components through the `ISchedulerKitConnection` interface.

[**IExecutor**](iexecutor.md)

An interface providing a protocol for objects that have executable tasks. It establishes a uniform method of execution, ensuring that any implementing object can be managed by the system's scheduler.

[**ISchedulerKitConnection**](ischedulerconnectionkit.md)

An essential bridge between various system objects and the `TaskScheduler`. This interface defines the protocol for how different entities, be it tasks or devices, integrate and interact with the core time management system.

[**Task**](task.md)

Represents an individual unit of work or operation scheduled to be executed at a particular time. With its functionality to be set on a recurring or one-off basis, the Task class is foundational to the operation of the Uniot Core system.

[**SchedulerTask**](schedulertask.md)

An enhancement of the `Task`, integrating the `IExecutor` interface. This allows for more flexible task definitions, including the ability to set how many times the task is repeated and ensuring tasks can be executed with contextual parameters.

### Integration

By implementing the provided interfaces (`IExecutor` and `ISchedulerKitConnection`), any module or device can become part of the scheduling system. This integration fosters a consistent and efficient approach to time management within the Uniot Core. Emphasizing the importance of the `TaskScheduler`, it's the main time management of the whole Uniot Core, acting as the backbone of timely operations. Any modules or components designed to operate within the Uniot Core system's time-based framework should consider integrating with these classes to ensure optimal performance.
