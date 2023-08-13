# Utils

The `Utils` section within Uniot Core consists of a set of utility classes and functions that facilitate various common and specific operations required throughout the platform. These utilities improve code reusability and maintainability by encapsulating common functionalities. Let's explore the components:

**ArrayBuilder**

A dynamic array management class, `ArrayBuilder` helps in creating, modifying, and managing arrays with ease. It allows developers to add, remove, and manipulate array elements flexibly without delving deep into manual memory management.

**Bytes**

A class that simplifies byte-level operations, `Bytes` is essential for tasks like bit manipulation and conversion of data types to byte arrays. This becomes especially handy when handling data serialization and transmission over the network.

[**ClearQueue**](clearqueue.md)

As the name suggests, `ClearQueue` provides functionality to manage queues efficiently. It ensures that queues don't overflow and can be purged as needed, promoting effective memory management.

[**IterableQueue**](iterablequeue.md)

`IterableQueue` extends basic queue functionalities with the capability to iterate over the queue's elements seamlessly. This class aids in tasks that require traversal and manipulation of queued data.

[**LimitedQueue**](limitedqueue.md)

This class helps in managing queues with a size restriction. `LimitedQueue` automatically handles overflow by purging older entries when a limit is reached, ensuring that the system remains responsive and efficient.

**LinkRegisterRecord**

Serving as a record keeper, this class assists in registering and managing links within the system.

**LinksRegister**

Building upon `LinkRegisterRecord`, `LinksRegister` offers an advanced management system for multiple link records. It provides an interface to add and retrieve link records, fostering efficient link management.

**LinksRegisterProxy**

This class acts as an intermediary for `LinksRegister`, allowing you to name the register during initialization.

**Map**

An implementation of the map data structure, this class aids in storing key-value pairs. `Map` streamlines tasks like data lookup, insertion, and removal, ensuring quick access and management of data.

**StringUtils**

The `StringUtils` class provides a set of functionality for manipulating strings.
