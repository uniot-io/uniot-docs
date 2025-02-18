# Special

Special blocks provide essential control over program execution and event handling in your IoT system. These blocks enable you to:

- Control program timing and execution
- Handle MQTT events
- Manage program state
- Create event-driven behaviors

## task

<div align="left"><figure><img src="../../../.gitbook/assets/special_main.png" alt=""><figcaption></figcaption></figure></div>

Creates a recurring task that executes at specified intervals. This is the primary execution loop required in every script - only one task block is allowed per script as it serves as the main program loop.

**Parameters:**

- **Iterations** (Number): How many times to run (0 for infinite)
- **Interval** (Number): Time between executions in milliseconds

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/special_task_example.png" alt=""><figcaption>Read temperature every 5 seconds and send an event with the value</figcaption></figure></div>

## task pass

<div align="left"><figure><img src="../../../.gitbook/assets/special_iterator.png" alt=""><figcaption></figcaption></figure></div>

Returns the current task iteration count. For infinite tasks (0 iterations), returns -1.

**Returns:**

- **Number** (Number): -1 if infinite; otherwise a **countdown from n-1 to 0**

{% hint style="warning" %}

An iterator can not be used outside the task block.

<div align="left"><figure><img src="../../../.gitbook/assets/special_iterator_outside.png" alt=""><figcaption></figcaption></figure></div>

{% endhint %}

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/special_task_pass_example.png" alt=""><figcaption>Create LED patterns based on iteration</figcaption></figure></div>

{% hint style="info" %}

A custom iterator implementation.

<div align="left"><figure><img src="../../../.gitbook/assets/special_iterator_custom.png" alt=""><figcaption></figcaption></figure></div>

{% endhint %}

## is event

<div align="left"><figure><img src="../../../.gitbook/assets/special_is_event.png" alt=""><figcaption></figcaption></figure></div>

Checks if a specific MQTT event exists in the queue.

**Parameters:**

- **Event Name** (String): Name of the event to check

**Returns:**

- **Boolean**: `#t` if event exists, `()` if not

{% hint style="warning" %}

This block will return true until you retrieve and remove the value using the pop event block.

{% endhint %}

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/special_is_event_example.png" alt=""><figcaption>Check and retrieve an event</figcaption></figure></div>

## pop event

<div align="left"><figure><img src="../../../.gitbook/assets/special_pop_event.png" alt=""><figcaption></figcaption></figure></div>

Retrieves and removes the oldest event of the specified type from the queue.

**Parameters:**

- **Event Name** (String): Name of the event to retrieve

**Returns:**

- **Value**: The event value, or `()` if no event exists

{% hint style="warning" %}

The event payload is always of type Number.

{% endhint %}

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/special_is_event_example.png" alt=""><figcaption>Check and retrieve an event</figcaption></figure></div>

## push event

<div align="left"><figure><img src="../../../.gitbook/assets/special_push_event.png" alt=""><figcaption></figcaption></figure></div>

Sends an event with a value to the MQTT broker.

**Parameters:**

- **Event Name** (String): Name of the event
- **Value**: Value to send (number or boolean)

{% hint style="warning" %}

The event payload is always of type Number. Boolean values are converted to 1 or 0.

{% endhint %}

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/special_push_event_example.png" alt=""><figcaption>Send sensor readings</figcaption></figure></div>
