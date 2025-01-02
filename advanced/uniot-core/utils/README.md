# Utils

The `Utils` section within Uniot Core consists of a set of utility classes and functions that facilitate various common and specific operations required throughout the platform. These utilities improve code reusability and maintainability by encapsulating common functionalities. Let's explore the components:

[**Array**](../../../uniot-core/utils/array.md)

A dynamic array management class, `Array` helps in creating, modifying, and managing arrays with ease. It allows developers to add, remove, and manipulate array elements flexibly without delving deep into manual memory management.

[**Bytes**](../../../uniot-core/utils/bytes.md)

A class that simplifies byte-level operations, `Bytes` is essential for tasks like bit manipulation and conversion of data types to byte arrays. This becomes especially handy when handling data serialization and transmission over the network.

[**GlobalBufferMemoryManager**](../../../uniot-core/utils/globalbuffermemorymanager.md)

A class is a sophisticated memory management utility designed to handle dynamic memory allocation within a predefined global buffer. This manager optimizes memory usage by maintaining a free list of memory blocks, allowing for efficient allocation, deallocation, and resizing of memory segments.

[**ClearQueue**](clearqueue.md)

As the name suggests, `ClearQueue` provides functionality to manage queues efficiently. It ensures that queues don't overflow and can be purged as needed, promoting effective memory management.

[**IterableQueue**](iterablequeue.md)

`IterableQueue` extends basic queue functionalities with the capability to iterate over the queue's elements seamlessly. This class aids in tasks that require traversal and manipulation of queued data.

[**LimitedQueue**](limitedqueue.md)

This class helps in managing queues with a size restriction. `LimitedQueue` automatically handles overflow by purging older entries when a limit is reached, ensuring that the system remains responsive and efficient.

[**Singleton**](../../../uniot-core/utils/singleton.md)

A utility implements the Singleton design pattern, ensuring that a class has only one instance throughout the application's lifecycle and providing a global point of access to that instance. This pattern is particularly beneficial in scenarios where a single shared resource or manager is required.

[**TypeId**](../../../uniot-core/utils/typeid.md)

`TypeId` provides a lightweight and efficient mechanism for runtime type identification and safe type casting without relying on traditional C++ Run-Time Type Information (RTTI).

**LinkRegisterRecord**

Serving as a record keeper, this class assists in registering and managing links within the system.

**LinksRegister**

Building upon `LinkRegisterRecord`, `LinksRegister` offers an advanced management system for multiple link records. It provides an interface to add and retrieve link records, fostering efficient link management.

**LinksRegisterProxy**

This class acts as an intermediary for `LinksRegister`, allowing you to name the register during initialization.

[**Map**](../../../uniot-core/utils/map.md)

An implementation of the map data structure, this class aids in storing key-value pairs. `Map` streamlines tasks like data lookup, insertion, and removal, ensuring quick access and management of data.

**StringUtils**

The `StringUtils` class provides a set of functionality for manipulating strings.
