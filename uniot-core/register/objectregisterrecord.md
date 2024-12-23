# ObjectRegisterRecord

The `ObjectRegisterRecord` class serves as a foundational component for managing object records within the Uniot Register module. It tracks the active status of registered objects, ensuring that only valid and existing records are accessible, thereby enhancing the integrity and reliability of object management.

**Methods:**

* **`ObjectRegisterRecord()`**\
  Constructs an `ObjectRegisterRecord` instance and registers it within the global registry.

* **`~ObjectRegisterRecord()`**\
  Destructs an `ObjectRegisterRecord` instance and unregisters it from the global registry.

* **`static bool exists(ObjectRegisterRecord *record)`**\
  Checks whether a given object record exists within the global registry.

**Private Members:**

* **`static ClearQueue<ObjectRegisterRecord *> sRegisteredLinks`**\
  A static queue that holds pointers to all active `ObjectRegisterRecord` instances, facilitating global tracking and validation.
