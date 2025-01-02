---
description: A Lightweight and Efficient Queue Implementation
---

# ClearQueue

The `ClearQueue` class is a templated, lightweight, and memory-efficient implementation of the queue data structure. Unlike the `std::queue` in the C++ standard library that often requires more resources, this class has been optimized for use in embedded systems like those used in the Uniot Core project.

### **Purpose and Benefits**

* **Lightweight and Resource-Efficient**: Being specially crafted for systems with limited resources, `ClearQueue` offers a simplified interface and consumes less memory.
* **Uniqueness Handling**: Offers functionality to handle unique values in the queue.
* **Flexible Operations**: Provides functions for adding, removing, inspecting, and iterating over the elements.
* **Error Handling**: Offers a mechanism to provide error codes for certain operations, allowing for better control and robustness.

### Class Methods

**Constructor and Destructor**:

* `ClearQueue()`: Initializes the queue with empty states.
* `~ClearQueue()`: Cleans up the queue, releasing any allocated memory.

**Push Operations**:

* `push(const T value)`: Adds the specified value to the end of the queue.
* `pushUnique(const T value)`: Adds the value to the queue only if it doesn't already exist. Returns `true` if the value was added.

**Pop and Peek Operations**:

* `hardPop()`: Removes and returns the front element from the queue without any checks.
* `hardPeek() const`: Returns the front element without removing it.
* `pop(const T errorCode)`: Removes and returns the front element. If the queue is empty, it returns the provided error code.
* `peek(const T errorCode) const`: Returns the front element without removing it. If the queue is empty, returns the provided error code.

**Element Management**:

* `removeOne(const T value)`: Removes the first occurrence of the specified value from the queue. Returns `true` if successful.
* `contains(const T value) const`: Checks if the queue contains the specified value.

**Queue State Checks**:

* `isEmpty() const`: Returns `true` if the queue is empty.

**Iteration**:

* `forEach(VoidCallback callback)`: Iterates over each element in the queue, executing the provided callback for each element.
