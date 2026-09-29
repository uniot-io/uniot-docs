# Logger

The Logger is the Sandbox's output pane. It shows the interpreter's report on the last run of your script — when you compile it, or while it runs in the [Emulator](emulator.md) — with these parts:

- **`states`** - The run's timeline: every interaction with a primitive, such as a value read from or written to a pin, every event sent or received, and every line printed with the **print** block from the "Text" section, in the order they happened.
- **`log`** - Only the lines the script printed.
- **`out`** - The value the script finished with.
- **`err`** - If the script stopped with an error, its message and where in the code it occurred.

While the Emulator runs, the Logger follows it. The Emulator also shows printed lines and errors on their own, in its Logs panel.

The Logger is an essential tool for understanding the behavior of your script and ensuring its reliability before deployment.
