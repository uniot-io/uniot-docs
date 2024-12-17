# Loops

The Loops section provides blocks that enable you to repeatedly execute a set of instructions, making your programs more efficient and powerful. Instead of manually duplicating code for each iteration, you can use loops to:

* Run certain actions a specific number of times.
* Continue processing while a given condition is true.
* Repeat a block of code until a particular event occurs.

## repeat

The simplest "repeat" block runs the code in its body the specified number of times. For example, the block on the image will print "Hello!" ten times.

### Parameters

* **Count** (Number): How many times to repeat.

## repeat while

Repeats the enclosed blocks as long as a condition is `true`.

### Parameters

* **Condition** (Boolean)

## repeat until

Repeats the enclosed blocks until a condition is `true`.

### Parameters

* **Condition** (Boolean)

## iterator

A block that returns an [iterator](https://en.wikipedia.org/wiki/For_loop#Loop_counters).

### Returns

* **Iterator** (number)

> _**NOTE**_: An iterator can not be used outside the loop.
