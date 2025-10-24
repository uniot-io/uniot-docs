# Math

Math blocks provide numerical operations and calculations for your scripts. Use these blocks to perform arithmetic, apply mathematical functions, and manipulate numeric values from sensors or variables.

## value

<div align="left"><figure><img src="../../../.gitbook/assets/math_value.png" alt=""><figcaption></figcaption></figure></div>

A numeric constant. Use this block to provide fixed numbers for calculations, comparisons, or as parameters to other blocks.

**Parameters:**

- **Value** (Number): Enter any numeric value (integers or decimals)

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_value_example.png" alt=""><figcaption>Define temperature thresholds</figcaption></figure></div>

## math operation

<div align="left"><figure><img src="../../../.gitbook/assets/math_operation.png" alt=""><figcaption></figcaption></figure></div>

Applies a single-value mathematical operation. Choose from absolute value (removes sign) or negation (flips positive to negative and vice versa).

**Parameters:**

- **Operation**: Select `abs` (absolute value) or `-` (negate)
- **Value** (Number): The number to operate on

**Returns:**

- **Number**: The result of the operation

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_operation_example.png" alt=""><figcaption>Temperature difference calculation</figcaption></figure></div>

## arithmetic

<div align="left"><figure><img src="../../../.gitbook/assets/math_arithmetic.png" alt=""><figcaption></figcaption></figure></div>

Performs basic arithmetic operations between two numbers.

**Parameters:**

- **Left Value** (Number): The first number
- **Operator**: Choose `+` (add), `-` (subtract), `×` (multiply), `÷` (divide), `^` (power)
- **Right Value** (Number): The second number

**Returns:**

- **Number**: The result of the calculation

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_arithmetic_example.png" alt=""><figcaption>Convert raw sensor value to voltage</figcaption></figure></div>

## number condition

<div align="left"><figure><img src="../../../.gitbook/assets/math_number_condition.png" alt=""><figcaption></figcaption></figure></div>

Checks whether a number meets a specific condition. Use this for pattern detection or periodic actions.

**Parameters:**

- **Value** (Number): The number to check
- **Condition**: Select `even`, `odd`, `positive`, `negative`, `whole`, `divisible by`

**Returns:**

- **Boolean**: `#t` (true) if the condition is met, `()` (false) otherwise

**Example:**

<div><figure><img src="../../../.gitbook/assets/math_number_condition_example.png" alt=""><figcaption>Read sensor value every 5th script execution</figcaption></figure></div>

## remainder

<div align="left"><figure><img src="../../../.gitbook/assets/math_remainder.png" alt=""><figcaption></figcaption></figure></div>

Calculates the remainder after dividing one number by another (modulo operation). Useful for creating repeating patterns or detecting multiples.

**Parameters:**

- **Dividend** (Number): The number to be divided
- **Divisor** (Number): The number to divide by

**Returns:**

- **Number**: The remainder of the division

**Example:**

<div><figure><img src="../../../.gitbook/assets/loops_iterator_example.png" alt=""><figcaption>Alternate on/off pattern for multiple LEDs</figcaption></figure></div>
