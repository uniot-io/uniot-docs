# Variables

Variables allow you to store, retrieve, and manipulate data within the script. They are essential for keeping track of changing values, such as sensor readings, user inputs, or counters.

{% hint style="info" %}

Note: Before using a variable, you typically create it through a corresponding section in the toolbox. Once created, it can be used and modified throughout your program. Variables are case-sensitive and should have meaningful names to make your code easier to understand.

{% endhint %}

## set

<div align="left"><figure><img src="../../../.gitbook/assets/variables_set.png" alt=""><figcaption></figcaption></figure></div>

Creates a new variable or changes an existing variable's value.

**Parameters:**

- **Variable Name** (String): The name of the variable to set.
- **Value** (Any type): The value to store in the variable.

**Example:**

<div><figure><img src="../../../.gitbook/assets/variables_set_example.png" alt=""><figcaption>Setting variables</figcaption></figure></div>

## get

<div align="left"><figure><img src="../../../.gitbook/assets/variables_get.png" alt=""><figcaption></figcaption></figure></div>

Retrieves the current value of a variable.

**Parameters:**

- **Variable Name** (String): The name of the variable whose value you want to access.

**Returns:**

- **Any type**: The current value of the specified variable.

**Example:**

<div><figure><img src="../../../.gitbook/assets/variables_get_example.png" alt=""><figcaption>Getting variable values</figcaption></figure></div>

## change

<div align="left"><figure><img src="../../../.gitbook/assets/variables_change.png" alt=""><figcaption></figcaption></figure></div>

Modifies a numeric variable by adding a value to it.

**Parameters:**

- **Variable Name** (String): The name of the variable to modify.
- **Value** (Number): The amount to add to the variable.

**Example:**

<div><figure><img src="../../../.gitbook/assets/variables_change_example.png" alt=""><figcaption>Modifying variables</figcaption></figure></div>

## Dropdown Menu

<div align="left"><figure><img src="../../../.gitbook/assets/variables_dropdown.png" alt=""><figcaption></figcaption></figure></div>

The variable dropdown menu provides options to:

- Select existing variables
- Rename selected variable
- Delete selected variable

{% hint style="warning" %}

Renaming or deleting a variable affects all blocks that use that variable.

{% endhint %}
