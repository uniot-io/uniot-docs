# Variables Blocks

Variables allow you to store, retrieve, and manipulate data within the script. They are essential for keeping track of changing values, such as sensor readings, user inputs, or counters.

**Note:** Before using a variable, you typically select or create it through a dropdown in the block. Once created, it can be used and modified throughout your program. Variables are case-sensitive and should have meaningful names to make your code easier to understand.

## set

Assigns a specified value to a variable. If the variable does not yet exist, this action creates it.

### Parameters

* **Variable Name** (String): The name of the variable to set.
* **Value** (Any type): The value to store in the variable.

## get

Retrieves the current value stored in a variable.

### Parameters

* **Variable Name** (String): The name of the variable whose value you want to access.

### Returns

* **Any type**: The current value of the specified variable.

## change

Modifies a numeric variable by adding a specified amount to its current value. This is a shorthand operation for incrementing or decrementing numerical values stored in variables.

### Parameters

* **Variable Name** (String): The name of the variable to change.
* **Amount** (Number): The value to add to the variable’s current value.

## Dropdown menu

Clicking on a variable's dropdown symbol (triangle) gives the following menu:

The menu provides the following options.

* the names of all existing variables defined in the program.
* "Rename variable...", changes the name of this variable wherever it appears in the program. Selecting this option opens a prompt for the new name.
* "Delete the variable...", deletes all blocks that reference this variable wherever it appears in the program.
