# Button

The `Button` class represents a hardware button within the Uniot Core. It provides mechanisms for detecting clicks and long presses, executing callbacks in response to these events, and managing internal state for debouncing and event triggering. By encapsulating button functionality, `Button` simplifies the integration of physical buttons.

**Methods:**

* **`Button(uint8_t pin, uint8_t activeLevel, uint8_t longPressTicks, ButtonCallback commonCallback = nullptr, uint8_t autoResetTicks = 100)`**\
  Constructs a `Button` instance with specified pin configurations and callback functions. Initializes the pin mode and sets up parameters for long press detection and automatic event resetting.

* **`bool resetClick()`**\
  Resets the click event flag. Returns `true` if a click was previously detected, `false` otherwise.

* **`bool resetLongPress()`**\
  Resets the long press event flag. Returns `true` if a long press was previously detected, `false` otherwise.

* **`virtual void execute(short _) override`**\
  Executes the button state checking routine. Detects button state changes, determines if a click or long press event has occurred, and invokes the corresponding callbacks.

* **`virtual type_id getTypeId() const override`**\
  Returns the type identifier for the `Button` class, enabling type-safe casting and identification within the system.

**Private Members:**

* **`uint8_t mPin`**\
  Stores the GPIO pin number to which the button is connected.

* **`uint8_t mActiveLevel`**\
  Indicates the active level (HIGH or LOW) that signifies a button press.

* **`uint8_t mLongPressTicks`**\
  Specifies the number of ticks required to recognize a long press event.

* **`uint8_t mAutoResetTicks`**\
  Defines the number of ticks after which the event flags are automatically reset.

* **`bool mWasClick`**\
  Flags whether a click event has been detected.

* **`bool mWasLongPress`**\
  Flags whether a long press event has been detected.

* **`ButtonCallback OnLongPress`**\
  Callback function to be invoked when a long press event is detected.

* **`ButtonCallback OnClick`**\
  Callback function to be invoked when a click event is detected.

* **`bool mPrevState`**\
  Stores the previous state of the button for change detection.

* **`uint8_t mLongPressTicker`**\
  Ticker counting ticks towards recognizing a long press event.

* **`uint8_t mAutoResetTicker`**\
  Ticker counting ticks towards automatic event flag resetting.
