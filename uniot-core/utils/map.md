# Map

The `Map` utility provides a simple and efficient way to associate keys with values using an iterable queue structure. It offers dynamic key-value management while ensuring minimal memory overhead and optimal performance in resource-constrained environments.

**Key Features:**

- Dynamic storage of key-value pairs using an iterable queue.
- Simple interface for common map operations.
- Efficient memory usage suitable for embedded systems.
- Template-based design for flexibility with various data types.

**Template Parameters:**

* **`T_Key`**\
The type of the keys used to identify values within the map. Must support equality comparison (operator==).

* **`T_Value`**\
The type of the values associated with keys in the map.

**Methods:**

* **`bool put(const T_Key& key, const T_Value& value)`**\
Inserts a key-value pair into the map. If the key already exists, the method does not overwrite the existing value and returns false to indicate the insertion was unsuccessful.

* **`const T_Value& get(const T_Key& key, const T_Value& defaultValue = {}) const`**\
Retrieves the value associated with a specific key.

* **`bool exist(const T_Key& key) const`**\
Checks whether a specific key exists within the map.

* **`bool remove(const T_Key& key)`**\
Removes a key-value pair from the map based on the provided key.
