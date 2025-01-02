---
description: A Size-Capped Queue Implementation
---

# LimitedQueue

The `LimitedQueue` class is a specialization of `ClearQueue` that adds functionality to limit the size of the queue. This class ensures that the queue does not grow beyond a specified size limit, providing better control over memory utilization.

### Class Methods

**Constructor:**

* **`LimitedQueue()`**: Initializes an empty `LimitedQueue` object with zero limit and size.

**Accessor and Mutator Methods:**

* **`size_t limit()`**: Returns the current size limit of the queue.
* **`size_t size()`**: Returns the current size of the queue (i.e., the number of elements it contains).
* **`void limit(size_t limit)`**: Sets the size limit for the queue. If the limit is set to a value less than the current size of the queue, excess elements are removed from the front of the queue.

**Element Operations:**

* **`bool isFull()`**: Checks if the queue has reached its size limit.
* **`void pushLimited(const T value)`**: Pushes a new value into the queue, respecting the size limit. If adding the value would exceed the size limit, the oldest value in the queue is removed.
* **`T popLimited(const T errorCode)`**: Pops a value from the queue. Also decrements the size counter.

**Internal Logic:**

* **`void applyLimit()`**: Removes excess elements from the front of the queue until it's within the size limit.
* **`size_t calcSize()`**: Recalculates and updates the size of the queue by iterating over all elements. Useful in scenarios where there's a potential discrepancy between the `mSize` value and the actual number of elements.

**Member Variables:**

* **`mLimit`**: Represents the size limit of the queue.
* **`mSize`**: Represents the current number of elements in the queue.

**Inherited Members:**

As `LimitedQueue` is derived from `ClearQueue`, it inherits all functionalities of the `ClearQueue` class.

