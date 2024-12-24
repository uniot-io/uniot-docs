# Visual Block Editor

Our Visual Block Editor is based on [Blockly](https://developers.google.com/blockly). With it, you can create scripts by assembling visual blocks. These scripts are then converted into LISP code and can be deployed to your IoT device.

## How It Works

1. **Arrange Blocks**: Drag and drop visual blocks to build your logic.
2. **Interact with hardware**: Handle hardware I/O, read data, and manipulate state with [Primitives](primitives.md)
3. **Interact with MQTT**: Handle events, push and pop event payloads, and integrate with external IoT services.
4. **Generate LISP**: Compile your script to get LISP code.

## Components

All blocks are organized into intuitive sections. Each section corresponds to a set of blocks designed for specific purposes, from performing basic arithmetic to handling hardware I/O and MQTT events.

* [**Logic**](logic.md): Includes blocks for boolean operations, comparisons, and conditional statements to control the flow of your scripts.
* [**Math**](math.md): Provides blocks for arithmetic, random number generation, and advanced mathematical functions.
* [**Loops**](loops.md): Enables repeating sequences of instructions based on conditions or specific counts.
* [**Text**](text.md): Contains blocks for creating, manipulating, and outputting text strings in your scripts.
* [**Lists**](lists.md): Offers tools to create and manipulate lists, allowing you to handle collections of data effectively.
* [**Variables**](variables.md): Allows you to store, retrieve, and modify values using named variables in your scripts.
* [**Functions**](functions.md): Lets you define reusable blocks of code with optional parameters and return values.
* [**Special**](special.md): Provides blocks for controlling the script execution flow and interacting with external MQTT events.
* [**Primitives**](primitives.md): Includes blocks for direct hardware interactions, such as reading sensor data or controlling actuators.
