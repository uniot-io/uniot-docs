# Loops

Loop blocks repeatedly execute code, eliminating the need to duplicate instructions. Use loops to process multiple sensor readings, generate patterns, handle collections of data, or create sequences of operations.

## repeat

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat.png" alt=""><figcaption></figcaption></figure></div>

Executes the enclosed code a fixed number of times. Use this when you know exactly how many iterations you need.

**Parameters:**

- **Count** (Number): Number of times to repeat

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_example.png" alt=""><figcaption>Average sensor reading</figcaption></figure></div>

## repeat while

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_while.png" alt=""><figcaption></figcaption></figure></div>

Repeats code as long as the condition remains true. The condition is checked before each iteration.

**Parameters:**

- **Condition** (Boolean): The condition to evaluate before each iteration

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_while_example.png" alt=""><figcaption>Process values while above threshold</figcaption></figure></div>

## repeat until

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_until.png" alt=""><figcaption></figcaption></figure></div>

Repeats code until the condition becomes true. The condition is checked after each iteration, so the loop always executes at least once.

**Parameters:**

- **Condition** (Boolean): The condition to evaluate after each iteration

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_until_example.png" alt=""><figcaption>Read until valid value received</figcaption></figure></div>

## iterator

<div align="left"><figure><img src="../../../.gitbook/assets/loops_iterator.png" alt=""><figcaption></figcaption></figure></div>

Returns the current iteration counter for the loop, starting from 0. Use this to create indexed operations or patterns.

**Returns:**

- **Number**: The current loop iteration (0, 1, 2, ...)

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/loops_iterator_example.png" alt=""><figcaption>Alternate on/off pattern for multiple LEDs</figcaption></figure></div>

{% hint style="warning" %}

This block only works inside a loop block. Using it elsewhere will cause an error.

<img src="../../../.gitbook/assets/loops_iterator_outside.png" alt="" data-size="original">

{% endhint %}
