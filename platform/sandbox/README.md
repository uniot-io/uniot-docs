# Sandbox

The Sandbox is your complete development environment for creating, testing, and deploying device logic. Write scripts that define how your devices behave, test them in a safe simulated environment, and deploy them to real hardware - all without leaving your browser.

## Overview

The Sandbox streamlines the entire device programming workflow:

1. **Develop** - Write logic using visual blocks or UniotLisp code
2. **Test** - Run and debug scripts in the emulator before deploying
3. **Monitor** - Track execution with real-time logging
4. **Deploy** - Upload verified scripts to your devices

This integrated approach eliminates the traditional compile-upload-debug cycle. Changes can be tested instantly in the emulator, dramatically reducing development time and preventing bugs from reaching production hardware.

## Development Tools

### Visual Editor vs. Code Editor

The Sandbox offers two ways to create device logic:

- **[Visual Editor](visual-editor/)** - A drag-and-drop block-based interface perfect for building logic without writing code. Ideal for rapid prototyping, learning, and creating straightforward device behaviors.

- **Code Editor** - A text-based editor for writing [UniotLisp](../../advanced/uniot-lisp/language-description.md) directly. Provides full language capabilities for complex logic, custom functions, and advanced device control.

{% hint style="warning" %}

**Important**: The Visual Editor and Code Editor operate in different modes. Once you manually edit UniotLisp code in the Code Editor, the Visual Editor becomes read-only to prevent conflicts. To return to Visual Editor mode, recompile your visual blocks - this will overwrite any manual code changes with the block-based version.

{% endhint %}

{% hint style="danger" %}

Compile the code only if you create the script in the [Visual Editor](visual-editor/). If you wrote the UniotLisp code directly, compiling will replace your code with the generated code from the visual blocks.

{% endhint %}

### Testing and Debugging

- **[Emulator](emulator.md)** - A virtual device environment that simulates hardware behavior. Test your scripts, validate logic, and catch errors before deployment. The emulator mimics real device states, sensor inputs, and timing, providing confidence that your code will work correctly on actual hardware.

- **[Logger](logger.md)** - A real-time logging console that displays script execution details, variable values, errors, and custom debug messages. Essential for understanding what your code is doing and troubleshooting issues both in the emulator and on deployed devices.

## Typical Workflow

1. **Create a new script** in the Sandbox
2. **Build your logic** using the Visual Editor or Code Editor
3. **Run in the emulator** to verify behavior
4. **Check the logger** for any errors or unexpected behavior
5. **Refine and iterate** until the script works as intended
6. **Deploy to your device** for real-world operation

The Sandbox keeps your development organized and efficient, with all tools accessible in a single, cohesive interface.
