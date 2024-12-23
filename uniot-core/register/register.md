# Register

The `Register` class is a versatile and generalized template class within the Uniot Register module, designed to handle the registration and management of various system entities.

**Methods:**

* **`bool setRegister(const String& name, const T* values, size_t count)`**\
  Sets the register with the specified name and array of values.

* **`bool addToRegister(const String& name, const T& value)`**\
  Adds a single value to an existing register. If the register does not exist, it will be created with a default capacity.

* **`bool getRegisterValue(const String& name, size_t idx, T& outValue) const`**\
  Retrieves a value from the register by name and index with bounds checking.

* **`bool setRegisterValue(const String& name, size_t idx, const T& value)`**\
  Sets a value in the register by name and index with bounds checking.

* **`size_t getRegisterLength(const String& name) const`**\
  Gets the number of values in the specified register.

* **`void iterateRegisters(IteratorCallback callback) const`**\
  Iterates through all registers and calls the provided callback function for each one.

**Private Members:**

* **`Map<String, SharedPointer<Array<T>>> mRegisterMap`**\
  A map associating each register name with its corresponding array of values, enabling efficient storage and retrieval.
