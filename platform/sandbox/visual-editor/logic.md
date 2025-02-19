# Logic

Logic blocks help you make decisions in your scripts based on conditions. Use logic to:

- Compare values
- Create conditional behaviors
- Combine multiple conditions
- Control program flow based on states

## value

<div align="left"><figure><img src="../../../.gitbook/assets/logic_value.png" alt=""><figcaption></figcaption></figure></div>

Represents a boolean value (`#t` for true or `()` for false).

**Parameters:**

- **Value** (Boolean): Boolean value to set.

**Returns:**

- **Boolean**: The selected Boolean value.

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_value_example.png" alt=""><figcaption>Set initial values</figcaption></figure></div>

## if

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if.png" alt=""><figcaption></figcaption></figure></div>

Executes enclosed blocks if the condition is true.

**Parameters:**

- **Condition** (Boolean): The condition to check

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if_example.png" alt=""><figcaption>Send event if button was clicked</figcaption></figure></div>

### Block Modification

Only the plain `if` block appears in the toolbox. To add `else if` and `else` clauses, click on the gear icon, which opens a new window:

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if_settings.png" alt=""><figcaption></figcaption></figure></div>

You can drag `else if` and `else` clauses under the `if` block, reorder them, and remove them as needed. When finished, click on the gear icon to close the window, as shown here:

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if_settings2.gif" alt=""><figcaption></figcaption></figure></div>

Note that the shape of the blocks allows any number of `else if` subblocks to be added but only up to one `else` block.

## comparison

<div align="left"><figure><img src="../../../.gitbook/assets/logic_comparison.png" alt=""><figcaption></figcaption></figure></div>

Compares two values using operators: `=`, `≠`, `<`, `>`, `≤`, `≥`

**Parameters:**

- **Left Value** (Number or comparable type): The first value to compare.
- **Right Value** (Number or comparable type): The second value to compare.
- **Operator** (Enum): The operator to use for the comparison.

**Returns:**

- **Boolean**: true if the comparison is satisfied, otherwise false.

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_comparison_example.png" alt=""><figcaption>Check humidity and send event when it is too high</figcaption></figure></div>

## and

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_and.png" alt=""><figcaption></figcaption></figure></div>

Returns true only if all conditions are true.

**Parameters:**

- **Input A** (Boolean): The first condition to check.
- **Input B** (Boolean): The second condition to check.

**Returns:**

- **Boolean**: true if both inputs are true, otherwise false.

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_and_example.png" alt=""><figcaption>Multiple condition check</figcaption></figure></div>

## or

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_or.png" alt=""><figcaption></figcaption></figure></div>

Returns true if any condition is true.

**Parameters:**

- **Input A** (Boolean): The first condition to check.
- **Input B** (Boolean): The second condition to check.

**Returns:**

- **Boolean**: true if at least one input is true, otherwise false.

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_or_example.png" alt=""><figcaption>Humidity alert</figcaption></figure></div>

## not

<div align="left"><figure><img src="../../../.gitbook/assets/logic_not.png" alt=""><figcaption></figcaption></figure></div>

Inverts a boolean value. If no input is provided, a value of true is assumed. Leaving an input empty is not recommended, however.

**Parameters:**

- **Input** (Boolean): The boolean value to invert.

**Returns:**

- **Boolean**: The inverted boolean value.

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_not_example.png" alt=""><figcaption>Toggle state by button click</figcaption></figure></div>
