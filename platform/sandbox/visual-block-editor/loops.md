# Loops

The Loops section provides blocks that enable you to repeatedly execute a set of instructions, making your programs more efficient and powerful. Instead of manually duplicating code for each iteration, you can use loops to:

* Run certain actions a specific number of times.
* Continue processing while a given condition is true.
* Repeat a block of code until a particular event occurs.

## repeat

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat.png" alt=""><figcaption></figcaption></figure></div>

The simplest "repeat" block runs the code in its body the specified number of times. For example, the block on the image will print "Hello!" ten times.

**Parameters:**

* **Count** (Number): How many times to repeat.

## repeat while

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_while.png" alt=""><figcaption></figcaption></figure></div>

Repeats the enclosed blocks as long as a condition is `true`.

**Parameters:**

* **Condition** (Boolean)

## repeat until

<div align="left"><figure><img src="../../../.gitbook/assets/loops_repeat_until.png" alt=""><figcaption></figcaption></figure></div>

Repeats the enclosed blocks until a condition is `true`.

**Parameters:**

* **Condition** (Boolean)

## iterator

<div align="left"><figure><img src="../../../.gitbook/assets/loops_iterator.png" alt=""><figcaption></figcaption></figure></div>

A block that returns an [iterator](https://en.wikipedia.org/wiki/For_loop#Loop_counters).

**Returns:**

* **Iterator** (number)

> _**NOTE**_: An iterator can not be used outside the loop.
>
> <img src="../../../.gitbook/assets/loops_iterator_outside.png" alt="" data-size="original">
