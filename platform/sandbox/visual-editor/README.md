# Visual Editor

The Visual Editor is a drag-and-drop interface for building device logic without writing code. Built on [Blockly](https://developers.google.com/blockly), it provides an intuitive way to create scripts by connecting visual blocks that represent programming concepts.

Behind the scenes, the Visual Editor automatically translates your block arrangements into [UniotLisp](../../../advanced/uniot-lisp/README.md) code. This approach makes IoT development accessible to beginners while remaining efficient for experienced developers who want to prototype quickly. Focus on application logic instead of syntax details.

## How It Works

1. **Drag blocks** from the toolbox into your workspace
2. **Connect blocks** together to build logic - blocks snap together when they're compatible
3. **Configure blocks** by filling in values, selecting options, or creating variables
4. **Test in the emulator** to verify behavior
5. **Compile to UniotLisp** when ready to deploy or view the generated code

The Visual Editor handles:

- **Hardware interactions** - Read sensors, control actuators, and manage device I/O with Primitive blocks
- **MQTT communications** - Handle events, access payloads, and publish messages
- **Program logic** - Conditions, loops, variables, functions, and data manipulation

## Block Categories

The Visual Editor organizes blocks into categories by function. Each category contains blocks designed for specific purposes:

- **[Special](special.md)**: Provides blocks for controlling the script execution flow and interacting with external MQTT events.
- **[Logic](logic.md)**: Includes blocks for boolean operations, comparisons, and conditional statements to control the flow of your scripts.
- **[Math](math.md)**: Provides blocks for arithmetic, random number generation, and advanced mathematical functions.
- **[Loops](loops.md)**: Enables repeating sequences of instructions based on conditions or specific counts.
- **[Text](text.md)**: Contains blocks for creating, manipulating, and outputting text strings in your scripts.
- **[Variables](variables.md)**: Allows you to store, retrieve, and modify values using named variables in your scripts.
- **[Functions](functions.md)**: Lets you define reusable blocks of code with optional parameters and return values.
- **[Primitives](primitives.md)**: Includes blocks for direct hardware interactions, such as reading sensor data or controlling actuators.
