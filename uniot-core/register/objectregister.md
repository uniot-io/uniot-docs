# ObjectRegister

The `ObjectRegister` class extends the generalized [`Register`](register.md) class to manage the registration and retrieval of complex system objects within the Uniot Core. It provides mechanisms to link named objects with unique identifiers and ensures that only valid and active records are accessible, enhancing the robustness and reliability of object management.

**Methods:**

* **`bool link(const String &name, RecordPtr link, uint32_t id = FOURCC(____))`**\
  Links a named object with a unique identifier, registering it within the system.

* **`template <typename T> T *get(const String &name, size_t index)`**\
  Retrieves a registered object of a specified type based on its name and index.
