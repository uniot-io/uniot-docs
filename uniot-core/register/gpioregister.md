# GpioRegister

The `GpioRegister` class specializes the generalized [`Register`](register.md) class to handle GPIO (General Purpose Input/Output) pin management within the Uniot system. It provides dedicated methods for configuring GPIO pins as digital or analog inputs and outputs, ensuring seamless integration with the underlying hardware.

**Methods:**

* **`template <typename... Args> void setDigitalInput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as digital inputs.

* **`template <typename... Args> void setDigitalOutput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as digital outputs.

* **`template <typename... Args> void setAnalogInput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as analog inputs.

* **`template <typename... Args> void setAnalogOutput(uint8_t first, Args... args)`**\
  Configures one or more GPIO pins as analog outputs.
