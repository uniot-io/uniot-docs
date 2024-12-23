# RegisterManagerProxy

The `RegisterManagerProxy` class acts as an intermediary between client classes and the central [`RegisterManager`](registermanager.md), facilitating controlled and streamlined interactions with registered entities. By abstracting the direct access to the `RegisterManager`, it promotes decoupled and modular design, enhancing the flexibility and maintainability.

**Methods:**

* **`RegisterManagerProxy(const String &name, RegisterManager *reg)`**\
  Constructs a `RegisterManagerProxy` instance associated with a specific register name and a pointer to the `RegisterManager`.

* **`bool getGpio(size_t index, uint8_t &outValue) const`**\
  Retrieves the value of a GPIO pin from the associated register by index.

* **`template <typename T> T *getObject(size_t index)`**\
  Retrieves a registered object of a specified type from the associated register by index.

**Private Members:**

* **`String mName`**\
  Stores the name of the register associated with the proxy, ensuring targeted access.

* **`RegisterManager *mpRegister`**\
  Pointer to the central `RegisterManager` instance, facilitating interactions with the register.
