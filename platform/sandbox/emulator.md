# Emulator

The Emulator is a virtual testing environment that simulates device hardware behavior, allowing you to validate scripts before deploying to physical devices. Test your logic, verify pin interactions, and debug issues in a safe, controlled environment where mistakes don't risk damaging hardware.

## How It Works

When you run a script in the Emulator, it creates virtual representations of all primitives used in your code. These components mirror real hardware behavior - digital pins, analog sensors, buttons, and custom primitives - letting you interact with them as if working with actual devices.

You can optionally select a specific device to emulate. When a device is selected, the Emulator configures itself to match that device's hardware profile. Without a device selection, it generates components based on the primitives defined in your script.

## Using the Emulator

1. **Write or load your script** in the Sandbox
2. **Start the emulator** - it analyzes your script and generates the necessary components
3. **Interact with the components** - toggle switches, adjust knobs, click buttons
4. **Monitor the logger** to see how your script responds
5. **Iterate and refine** until behavior matches your expectations

The Emulator updates in real-time, immediately reflecting changes in both your interactions and your script's output.

## Emulator Components

Each component in the Emulator represents a specific type of hardware primitive. Below are the available components and how to use them.

### Digital Read

<div align="left"><figure><img src="../../.gitbook/assets/digital_read.png" alt=""><figcaption></figcaption></figure></div>

Simulates a digital input pin that can be in either HIGH (1) or LOW (0) state. Click the toggle to switch between states and observe how your script responds to digital input changes.

**Use cases**: Testing button inputs, digital sensors, limit switches, or any script logic that reads digital pin states.

### Digital Write

<div align="left"><figure><img src="../../.gitbook/assets/digital_write.png" alt=""><figcaption></figcaption></figure></div>

Displays the current state of a digital output pin controlled by your script. Shows HIGH (1) or LOW (0) state, updating in real-time as your script executes digital write commands.

**Use cases**: Verifying LED control, relay switching, motor enable/disable signals, or any digital output behavior.

### Analog Read

<div align="left"><figure><img src="../../.gitbook/assets/analog_read.png" alt=""><figcaption></figcaption></figure></div>

Simulates an analog input pin with a rotatable knob. Adjust the knob to generate values between 0 and 1023, mimicking real analog sensors that output variable voltage levels.

**Use cases**: Testing temperature sensors, light sensors, potentiometers, pressure sensors, or any analog input processing logic.

### Analog Write

<div align="left"><figure><img src="../../.gitbook/assets/analog_write.png" alt=""><figcaption></figcaption></figure></div>

Displays the current analog output value (0-1023) being sent to a pin by your script. Shows PWM duty cycle or DAC output levels in real-time as your script executes.

**Use cases**: Verifying LED brightness control, motor speed regulation, servo positioning, or any PWM-based output control.

### Button Clicked

<div align="left"><figure><img src="../../.gitbook/assets/button_clicked.png" alt=""><figcaption></figcaption></figure></div>

Simulates a physical pushbutton with press-and-release behavior. Click to trigger a button press event in your script, testing event-driven logic without physical hardware.

**Use cases**: Testing user interface interactions, event handlers, menu navigation, emergency stops, or any button-triggered functionality.

### User Primitive

<div align="left"><figure><img src="../../.gitbook/assets/user_primitive.png" alt=""><figcaption></figcaption></figure></div>

Custom primitives you define in your script are automatically generated as interactive components in the Emulator. Each user primitive displays its input parameters with current values and types, and allows you to configure what it returns to your script.

**Use cases**: Testing custom sensor drivers, protocol handlers, communication interfaces, or any custom functionality you've implemented as a primitive.

#### Configuring Return Values

Click the gear icon on a user primitive to open the configuration modal. Here you can control what the primitive returns when called by your script:

**Return Value Options:**

- **Enable/Disable** - Toggle whether the primitive returns a value
- **Return Type** - Select from Bool, Int, Symbol, or other supported types
- **Value Definition**:
  - **Static value** - Enter a fixed return value for predictable testing
  - **Dynamic function** - Write a JavaScript function that computes the return value based on parameters or logic

The JavaScript function runs in a secure sandbox, protecting your environment while giving you flexibility to simulate complex behavior. For example, you could create a function that returns different values based on how many times it's been called, or combines input parameters in specific ways.

<div align="left"><figure><img src="../../.gitbook/assets/user_primitive_settings.gif" alt=""><figcaption></figcaption></figure></div>

This powerful feature lets you simulate real-world hardware complexity, testing edge cases and dynamic scenarios before deploying to actual devices.
