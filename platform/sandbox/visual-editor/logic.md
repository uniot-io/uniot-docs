# Logic

Logic blocks enable decision-making in your scripts. Use these blocks to compare values, create conditional behaviors, combine multiple conditions, and control program flow based on device states.

## value

<div align="left"><figure><img src="../../../.gitbook/assets/logic_value.png" alt=""><figcaption></figcaption></figure></div>

A boolean constant that represents true or false. Use this block to provide boolean values to conditions, comparisons, or variables.

**Parameters:**

- **Value** (Boolean): Select `true` or `false`

**Returns:**

- **Boolean**: `#t` for true, `()` for false (Lisp values)

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_value_example.png" alt=""><figcaption>Set initial values</figcaption></figure></div>

## if

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if.png" alt=""><figcaption></figcaption></figure></div>

Executes code conditionally based on whether a condition is true. This is the fundamental building block for creating decision-based behavior in your scripts.

**Parameters:**

- **Condition** (Boolean): The condition to evaluate

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if_example.png" alt=""><figcaption>Send event if button was clicked</figcaption></figure></div>

### Adding else if and else Clauses

The basic `if` block can be extended with additional conditions and fallback logic. Click the gear icon to open the configuration panel:

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if_settings.png" alt=""><figcaption></figcaption></figure></div>

Drag `else if` and `else` blocks from the left panel to build your conditional logic. You can add multiple `else if` clauses but only one `else` clause. Reorder or remove clauses as needed, then click the gear icon to close:

<div align="left"><figure><img src="../../../.gitbook/assets/logic_if_settings2.gif" alt=""><figcaption></figcaption></figure></div>

## comparison

<div align="left"><figure><img src="../../../.gitbook/assets/logic_comparison.png" alt=""><figcaption></figcaption></figure></div>

Compares two values using mathematical or equality operators. Use this to check sensor thresholds, compare states, or validate ranges.

**Parameters:**

- **Left Value** (Number): The first value to compare
- **Operator**: Choose from `=` (equal), `≠` (not equal), `<` (less than), `>` (greater than), `≤` (less or equal), `≥` (greater or equal)
- **Right Value** (Number): The second value to compare

**Returns:**

- **Boolean**: `#t` (true) if the comparison is satisfied, `()` (false) otherwise

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_comparison_example.png" alt=""><figcaption>Check humidity and send event when it is too high</figcaption></figure></div>

## and

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_and.png" alt=""><figcaption></figcaption></figure></div>

Returns true only if both conditions are true. Use this to combine multiple requirements that must all be satisfied.

**Parameters:**

- **Input A** (Boolean): The first condition
- **Input B** (Boolean): The second condition

**Returns:**

- **Boolean**: `#t` (true) if both inputs are true, `()` (false) otherwise

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_and_example.png" alt=""><figcaption>Multiple condition check</figcaption></figure></div>

## or

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_or.png" alt=""><figcaption></figcaption></figure></div>

Returns true if at least one condition is true. Use this when any of several conditions should trigger an action.

**Parameters:**

- **Input A** (Boolean): The first condition
- **Input B** (Boolean): The second condition

**Returns:**

- **Boolean**: `#t` (true) if at least one input is true, `()` (false) otherwise

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_operation_or_example.png" alt=""><figcaption>Humidity alert</figcaption></figure></div>

## not

<div align="left"><figure><img src="../../../.gitbook/assets/logic_not.png" alt=""><figcaption></figcaption></figure></div>

Inverts a boolean value, turning true into false and false into true. Use this to reverse conditions or check for the opposite of a state.

**Parameters:**

- **Input** (Boolean): The boolean value to invert

**Returns:**

- **Boolean**: `#t` (true) becomes `()` (false), and vice versa

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/logic_not_example.png" alt=""><figcaption>Toggle state by button click</figcaption></figure></div>
