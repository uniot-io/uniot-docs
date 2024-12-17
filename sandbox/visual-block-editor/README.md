# Visual Block Editor

Our Visual Block Editor is based on [Blockly](https://developers.google.com/blockly). With it, you can create scripts by assembling visual blocks. These scripts are then converted into LISP code and can be deployed to your IoT device.

## How It Works

1. **Arrange Blocks**: Drag and drop visual blocks to build your logic.
2. **Interact with hardware**: Handle hardware I/O, read data, and manipulate state with [Primitives](primitives.md)
3. **Interact with MQTT**: Handle events, push and pop event payloads, and integrate with external IoT services.
4. **Generate LISP**: Compile your script to get LISP code.

## Components

All blocks are organized into intuitive sections. Each section corresponds to a set of blocks designed for specific purposes, from performing basic arithmetic to handling hardware I/O and MQTT events.

* [Logic](logic.md)
* [Math](math.md)
* [Loops](loops.md)
* [Text](text.md)
* [Lists](lists-blocks.md)
* [Variables](variables-blocks.md)
* [Functions](functions.md)
* [Special](special-blocks.md)
* [Primitives](primitives.md)
