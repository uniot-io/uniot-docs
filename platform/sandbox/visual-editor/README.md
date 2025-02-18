# Visual Editor

The Visual Editor is a powerful tool that lets you create scripts using a drag-and-drop interface. Based on [Blockly](https://developers.google.com/blockly), it provides an intuitive way to create scripts without writing code directly. The editor automatically translates visual blocks into [UniotLisp](../../../advanced/uniot-lisp/README.md) code under the hood, making IoT development accessible to beginners while remaining efficient for experienced developers. This visual programming approach allows you to focus on your application logic rather than syntax details.

## How It Works

- **Arrange Blocks**: Drag and drop visual blocks to build your logic.
- **Interact with hardware**: Handle hardware I/O, read data, and manipulate state with Primitives
- **Interact with MQTT**: Handle events, push and pop event payloads.
- **Generate LISP**: Compile your script to get UniotLisp code.

## Components

All blocks are organized into intuitive sections. Each section corresponds to a set of blocks designed for specific purposes, from performing basic arithmetic to handling hardware I/O and MQTT events.

- **[Special](special.md)**: Provides blocks for controlling the script execution flow and interacting with external MQTT events.
- **[Logic](logic.md)**: Includes blocks for boolean operations, comparisons, and conditional statements to control the flow of your scripts.
- **[Math](math.md)**: Provides blocks for arithmetic, random number generation, and advanced mathematical functions.
- **[Loops](loops.md)**: Enables repeating sequences of instructions based on conditions or specific counts.
- **[Text](text.md)**: Contains blocks for creating, manipulating, and outputting text strings in your scripts.
- **[Variables](variables.md)**: Allows you to store, retrieve, and modify values using named variables in your scripts.
- **[Functions](functions.md)**: Lets you define reusable blocks of code with optional parameters and return values.
- **[Primitives](primitives.md)**: Includes blocks for direct hardware interactions, such as reading sensor data or controlling actuators.
