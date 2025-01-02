# LispPrimitives

The `LispPrimitives` namespace encapsulates a set of functions that implement fundamental hardware interactions as Lisp primitives within the Uniot Core. These primitives allow Lisp scripts to control hardware resources dynamically, such as digital and analog I/O operations and button interactions. Providing these primitives enables flexible and programmable hardware control through Lisp scripting.

**Methods:**

* **`Object dwrite(Root root, VarObject env, VarObject list)`**\
  Implements the digital write primitive, allowing Lisp scripts to set the state of a specified GPIO pin. It validates the pin number and desired state before performing the operation.

* **`Object dread(Root root, VarObject env, VarObject list)`**\
  Implements the digital read primitive, enabling Lisp scripts to read the current state of a specified GPIO pin. It validates the pin number and retrieves the pin's state.

* **`Object awrite(Root root, VarObject env, VarObject list)`**\
  Implements the analog write primitive, allowing Lisp scripts to set the analog value of a specified GPIO pin. It validates the pin number and value before performing the operation.

* **`Object aread(Root root, VarObject env, VarObject list)`**\
  Implements the analog read primitive, enabling Lisp scripts to read the current analog value of a specified GPIO pin. It validates the pin number and retrieves the pin's analog value.

* **`Object bclicked(Root root, VarObject env, VarObject list)`**\
  Implements the button clicked primitive, allowing Lisp scripts to check if a specific button has been clicked. It validates the button ID and retrieves the click status.
