---
description: Extension of ClearQueue for Element Iteration
---

# IterableQueue

The `IterableQueue` class inherits from the `ClearQueue` class, extending its functionality to allow iteration through the queue elements.

### Class Methods

**Iteration Control:**

* **`void begin()`**: Initializes the iterator to the beginning of the queue.
* **`bool isEnd()`**: Checks if the iterator has reached the end of the queue. Returns `true` if at the end.
* **`T next()`**: Moves the iterator to the next element in the queue and returns the value of the previous current element.
* **`T current()`**: Returns the value of the current element pointed to by the internal iterator without moving the iterator.

**Inherited Members:**

Since `IterableQueue` is derived from `ClearQueue`, it inherits all the functionalities of the `ClearQueue` class, including push, pop, peek, remove, containment check, and empty check operations.
