# Math

The Math section provides a range of blocks that enable you to perform numerical operations and transformations within your script. Whether you are adding two values, generating random numbers, or applying advanced mathematical functions like trigonometry or square roots, these blocks help bring numeric logic and computation into your IoT projects.

Using these blocks, you can:

- Perform basic arithmetic (addition, subtraction, multiplication, division).
- Apply mathematical functions (absolute value, negatiation, checking value for compliance with different conditions).
- Combine numeric operations with logic and loops to create complex, dynamic scripts.

## value

<div align="left"><figure><img src="../../../.gitbook/assets/math_value.png" alt=""><figcaption></figcaption></figure></div>

Represents a fixed numeric value.

**Parameters:**

- **Input Value** (Number): The numeric value to represent.

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_value_example.png" alt=""><figcaption>Define temperature thresholds</figcaption></figure></div>

## math operation

<div align="left"><figure><img src="../../../.gitbook/assets/math_operation.png" alt=""><figcaption></figcaption></figure></div>

Performs operations like absolute value or negation.

**Parameters:**

- **Input Value** (Number): The numeric value to operate on.

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_operation_example.png" alt=""><figcaption>Temperature difference calculation</figcaption></figure></div>

## arithmetic

<div align="left"><figure><img src="../../../.gitbook/assets/math_arithmetic.png" alt=""><figcaption></figcaption></figure></div>

Performs basic arithmetic: add (+), subtract (-), multiply (*), divide (/).

**Parameters:**

- **Left Value** (Number): The first numeric value.
- **Right Value** (Number): The second numeric value.

**Returns:**

- **Number** (Number): The result of the arithmetic operation.

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_arithmetic_example.png" alt=""><figcaption>Convert raw sensor value to voltage</figcaption></figure></div>

## number condition

<div align="left"><figure><img src="../../../.gitbook/assets/math_number_condition.png" alt=""><figcaption></figcaption></figure></div>

Checks numeric properties: even, odd, positive, negative, divisible by.

**Parameters:**

- **Input Value** (Number): The numeric value to check.

**Returns:**

- **Boolean** (Boolean): True if the condition is met, false otherwise.

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_number_condition_example.png" alt=""><figcaption>Read sensor value every 5th script execution</figcaption></figure></div>

## remainder check

<div align="left"><figure><img src="../../../.gitbook/assets/math_remainder.png" alt=""><figcaption></figcaption></figure></div>

Calculates the remainder after division.

**Parameters:**

- **Left Value** (Number): The first numeric value.
- **Right Value** (Number): The second numeric value.

**Returns:**

- **Number** (Number): The remainder of the division.

**Example:**

<div><figure><img src="../../../.gitbook/assets/loops_iterator_example.png" alt=""><figcaption>Alternate on/off pattern for multiple LEDs</figcaption></figure></div>
