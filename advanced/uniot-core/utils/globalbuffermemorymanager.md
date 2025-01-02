# GlobalBufferMemoryManager

The `GlobalBufferMemoryManager` class is a sophisticated memory management utility designed to handle dynamic memory allocation within a predefined global buffer. This manager optimizes memory usage by maintaining a free list of memory blocks, allowing for efficient allocation, deallocation, and resizing of memory segments.

**Key Features:**

- Custom memory allocator within a global buffer.
- Free list management for tracking available memory blocks.
- Support for allocation, deallocation, and resizing of memory blocks.
- Functions to retrieve total free memory and the size of the largest free block.
- Debugging capabilities to monitor memory operations and detect corruption.

**Methods:**

* **`static void initialize()`**\
Initializes the memory manager by setting up the free list to cover the entire global buffer.

* **`static void* allocate(size_t size)`**\
Allocates a block of memory of the specified size from the global buffer. Returns pointer to the allocated memory block if successful or `nullptr` if the allocation fails due to insufficient memory.

* **`static void deallocate(void* ptr)`**\
Deallocates a previously allocated block of memory, returning it to the free list.

* **`static void* reallocate(void* ptr, size_t newSize)`**\
Resizes a previously allocated memory block to a new size. Returns pointer to the resized memory block if successful or `nullptr` if the reallocation fails.

* **`static size_t getTotalFreeMemory()`**\
Retrieves the total amount of free memory available in the global buffer.

* **`static size_t getLargestFreeBlock()`**\
Retrieves the size of the largest contiguous free memory block in the global buffer.

**Private Members:**

* **`struct FreeBlock`**\
A structure representing a free memory block within the global buffer.

  * **`size_t size`**\
  Size of the free block in bytes.
  * **`FreeBlock* next`**\
  Pointer to the next free block in the free list.

* **`static constexpr bool DEBUG`**\
A compile-time flag for enabling or disabling debug logging within the memory manager. Default value: `false`

* **`static constexpr size_t BUFFER_SIZE`**\
Defines the size of the global buffer in bytes. Default value: 4096

* **`static uint8_t mGlobalBuffer[BUFFER_SIZE]`**\
The global buffer used for memory allocations.

* **`static FreeBlock* mFreeList`**\
Pointer to the head of the free list, managing available memory blocks.

**Private Methods:**

* **`size_t alignSize(size_t size)`**\
Aligns the requested size to a 4-byte boundary.

* **`bool _isPtrEqual(cn_cbor *cb, const void *ptr) const`**\
Checks if a given pointer is equal to the data pointer of a CBOR node.

* **`void _markAsDirty(bool updated)`**\
Marks the memory manager's state as dirty if an update occurs.
