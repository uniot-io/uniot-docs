# Array

The **Array** utility designed to provide a dynamic array structure similar to `std::vector` in C++. It offers efficient memory management, flexibility, and ease of use for handling collections of elements. By leveraging modern C++ features such as move semantics and type traits, the `Array` class ensures optimal performance and resource utilization.

**Key Features:**
- Dynamic resizing with automatic capacity management.
- Support for both copy and move semantics.
- Bounds-checked access methods.
- Efficient memory allocation strategies.
- Compatibility with trivially copyable types for optimized performance.

**Constructors and Destructor:**

* **`Array()`**\
Constructs an empty Array instance with no allocated memory.

* **`Array(size_t capacity)`**\
Constructs an Array with a predefined capacity, allocating memory for the specified number of elements.

* **`Array(size_t size, const T* values)`**\
Constructs an Array by copying elements from an existing C-style array.

* **`Array(Array&& other) noexcept`**\
Move constructor that transfers ownership of resources from another Array instance.

* **`~Array()`**\
Destructor that deallocates the memory used by the Array instance.

**Assignment Operators:**

* **`Array& operator=(Array&& other) noexcept`**\
Move assignment operator that transfers ownership of resources from another Array instance.

**Element Access:**

* **`T& operator[](size_t index)`**\
Provides unchecked access to the element at the specified index.

* **`const T& operator[](size_t index) const`**\
Provides read-only unchecked access to the element at the specified index.

* **`bool get(size_t index, T& outValue) const`**\
Provides bounds-checked access to retrieve the value at the specified index.

* **`bool set(size_t index, const T& value)`**\
Sets the value of the element at the specified index with bounds checking.

**Capacity Management:**

* **`size_t size() const`**\
Returns the number of elements currently stored in the array.

* **`size_t capacity() const`**\
Returns the total number of elements that can be stored in the array without reallocating.

* **`bool isEmpty() const`**\
Checks whether the array is empty.

* **`const T* raw() const`**\
Retrieves a const pointer to the underlying data array.

**Modifiers:**

* **`bool reserve(size_t newCapacity)`**\
Ensures that the array has at least the specified capacity. If the current capacity is less than newCapacity, the array is resized to accommodate.

* **`bool push(const T& value)`**\
Adds a new element to the end of the array using copy semantics. If the array is at capacity, it automatically resizes to accommodate the new element.

* **`bool push(T&& value)`**\
Adds a new element to the end of the array using move semantics, allowing for efficient transfer of resources from temporary objects.

* **`void clear()`**\
Removes all elements from the array, resetting its size to zero. Does not deallocate the memory, allowing for future reuse.

* **`bool shrink()`**\
Reduces the array's capacity to match its current size, freeing any unused memory. This can help minimize memory usage, especially after removing large numbers of elements.
