# Loops

Loops provides blocks that enable you to repeatedly execute a set of instructions, making your programs more efficient and powerful. Instead of manually duplicating code for each iteration, you can use loops to:

- Process multiple sensor readings
- Generate patterns for LED displays
- Handle collections of data
- Create sequences of operations

## repeat

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat.png" alt=""><figcaption></figcaption></figure></div>

Executes code a specific number of times.

**Parameters:**

- **Count** (Number): How many times to repeat

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_example.png" alt=""><figcaption>Avarage sensor reading</figcaption></figure></div>

## repeat while

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_while.png" alt=""><figcaption></figcaption></figure></div>

Repeats code as long as a condition is true.

**Parameters:**

- **Condition** (Boolean): The condition to check

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_while_example.png" alt=""><figcaption>Process values while above threshold</figcaption></figure></div>

## repeat until

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_until.png" alt=""><figcaption></figcaption></figure></div>

Repeats code until a condition becomes true.

**Parameters:**

- **Condition** (Boolean): The condition to check

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_until_example.png" alt=""><figcaption>Read until valid value received</figcaption></figure></div>

## iterator

<div align="left"><figure><img src="../../../.gitbook/assets/loops_iterator.png" alt=""><figcaption></figcaption></figure></div>

Returns the current loop iteration number (0-based).

**Returns:**

- **Iterator** (Number): The current loop iteration number

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_iterator_example.png" alt=""><figcaption>Alternate on/off pattern for multiple LEDs</figcaption></figure></div>

{% hint style="warning" %}

An iterator can not be used outside the loop.

<img src="../../../.gitbook/assets/loops_iterator_outside.png" alt="" data-size="original">

{% endhint %}
