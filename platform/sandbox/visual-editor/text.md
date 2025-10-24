# Text

Text blocks handle string operations and text-based data. Use these blocks to create text values, convert between strings and numbers, evaluate expressions, and send log messages.

## value

<div align="left"><figure><img src="../../../.gitbook/assets/text_value.png" alt=""><figcaption></figcaption></figure></div>

A text string constant. Use this block to create fixed text values for labels, messages, or event names.

**Parameters:**

- **Value** (String): Enter any text

**Returns:**

- **String**: The text value

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/text_value_example.png" alt=""><figcaption>Text value creation</figcaption></figure></div>

## quote

<div align="left"><figure><img src="../../../.gitbook/assets/text_quote.png" alt=""><figcaption></figcaption></figure></div>

Converts an expression or value into a string representation without evaluating it. Useful for capturing code as text.

**Parameters:**

- **Expression**: The value or expression to convert

**Returns:**

- **String**: The expression as text

## eval

<div align="left"><figure><img src="../../../.gitbook/assets/text_eval.png" alt=""><figcaption></figcaption></figure></div>

Evaluates a text string as UniotLisp code and returns the result. Use this to execute dynamic code or parse text-based expressions.

**Parameters:**

- **Expression** (String): Text containing UniotLisp code to evaluate

**Returns:**

- **Any**: The result of evaluating the expression

## print

<div align="left"><figure><img src="../../../.gitbook/assets/text_print.png" alt=""><figcaption></figcaption></figure></div>

Sends a log message to the MQTT broker. Messages appear on the device details page for monitoring and debugging.

**Parameters:**

- **Message** (String): The text to log

**Example:**

<div align="left"><figure><img src="../../../.gitbook/assets/text_print_example.png" alt=""><figcaption>Logging messages</figcaption></figure></div>
