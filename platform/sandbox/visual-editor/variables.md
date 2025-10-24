# Variables

Variables store and manage data in your scripts. Use variables to track changing values like sensor readings, counters, states, or calculated results.

{% hint style="info" %}

Create variables through the Variables section in the toolbox before using them. Variable names are case-sensitive - choose meaningful names to make your code easier to understand.

{% endhint %}

## set

<div align="left"><figure><img src="../../../.gitbook/assets/variables_set.png" alt=""><figcaption></figcaption></figure></div>

Assigns a value to a variable. If the variable doesn't exist, it's created automatically.

**Parameters:**

- **Variable**: Select from the dropdown or create a new variable
- **Value** (Any): The value to store

**Example:**

<div><figure><img src="../../../.gitbook/assets/variables_set_example.png" alt=""><figcaption>Setting variables</figcaption></figure></div>

## get

<div align="left"><figure><img src="../../../.gitbook/assets/variables_get.png" alt=""><figcaption></figcaption></figure></div>

Retrieves the current value stored in a variable.

**Parameters:**

- **Variable**: Select which variable to read

**Returns:**

- **Any**: The current value of the variable

**Example:**

<div><figure><img src="../../../.gitbook/assets/variables_get_example.png" alt=""><figcaption>Getting variable values</figcaption></figure></div>

## change

<div align="left"><figure><img src="../../../.gitbook/assets/variables_change.png" alt=""><figcaption></figcaption></figure></div>

Increments or decrements a numeric variable by adding a value to it. Use negative values to subtract.

**Parameters:**

- **Variable**: Select which variable to modify
- **Value** (Number): The amount to add (use negative for subtraction)

**Example:**

<div><figure><img src="../../../.gitbook/assets/variables_change_example.png" alt=""><figcaption>Modifying variables</figcaption></figure></div>

## Managing Variables

<div align="left"><figure><img src="../../../.gitbook/assets/variables_dropdown.png" alt=""><figcaption></figcaption></figure></div>

The variable dropdown menu in each block provides options to:

- **Select** existing variables from your script
- **Rename** the selected variable (updates all references)
- **Delete** the selected variable (removes from all blocks)

{% hint style="warning" %}

Renaming or deleting a variable affects **all blocks** that use it. Be careful when modifying variables used in multiple places.

{% endhint %}
