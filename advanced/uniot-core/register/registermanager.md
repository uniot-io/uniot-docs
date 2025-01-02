# RegisterManager

The `RegisterManager` class serves as the central orchestrator within the Uniot Register module, overseeing the registration and management of both GPIO pins and complex system objects.

**Methods:**

* **`template <typename... Args> void setDigitalInput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as digital inputs by forwarding the configuration to the [`GpioRegister`](gpioregister.md).

* **`template <typename... Args> void setDigitalOutput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as digital outputs by forwarding the configuration to the `GpioRegister`.

* **`template <typename... Args> void setAnalogInput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as analog inputs by forwarding the configuration to the `GpioRegister`.

* **`template <typename... Args> void setAnalogOutput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as analog outputs by forwarding the configuration to the `GpioRegister`.

* **`bool link(const String &name, RecordPtr link, uint32_t id = FOURCC(____))`**\
  Links a named object with a unique identifier by delegating the operation to the [`ObjectRegister`](objectregister.md).

* **`bool getGpio(const String &name, size_t index, uint8_t &outValue) const`**\
  Retrieves the value of a GPIO pin from the specified register by name and index.

* **`template <typename T> T *getObject(const String &name, size_t index)`**\
  Retrieves a registered object of a specified type based on its name and index by delegating the retrieval to the `ObjectRegister`.

* **`size_t getRegisterLength(const String &name) const`**\
  Gets the number of values in the specified register by querying both the `GpioRegister` and `ObjectRegister`.

* **`void serializeRegisters(CBORObject &obj)`**\
  Serializes the current state of all registers (both GPIO and object registers) into a CBOR object for persistent storage or transmission.

**Private Members:**

* **`ObjectRegister mObjectRegistry`**\
  Manages the registration and retrieval of complex system objects.

* **`GpioRegister mGpioRegistry`**\
  Manages the registration and configuration of GPIO pins.
