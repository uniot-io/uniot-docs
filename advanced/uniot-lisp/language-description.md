# Language Description

This section serves as a comprehensive guide to the UniotLisp language itself. It is intended for users who want to learn how to write programs in UniotLisp, understand its syntax, semantics, and utilize its features effectively.

## Language features

**UniotLisp** is a traditional Lisp interpreter. It reads one expression at a time from the standard input, evaluates it, and then prints out the return value of the expression. Here is an example of a valid input.

```lisp
(+ 1 2)
```

The above expression prints "3".

**UniotLisp** comes with a set of built-in primitives that provide essential functionalities. These primitives are the fundamental operations that can be used within Lisp code.

#### Literals

**UniotLisp** supports integer literals, `()`, `#t`, symbols, and list literals.

*   **Integer Literals**: Positive or negative integers.

    ```lisp
    42
    -7
    ```
*   **`()`**: Represents both the false value (`Nil`) and the empty list.

    ```lisp
    () ; Evaluates to false and an empty list
    ```
*   **`#t`**: Represents the true value (`True`). It's a preferred way to represent `true`, while any non-`()` value is considered true.

    ```lisp
    #t ; Evaluates to true
    ```
*   **Symbols**: Objects with unique names used to represent identifiers. Since **UniotLisp** does not have a string type, symbols are sometimes used as substitutes for strings.

    ```lisp
    x
    my-function
    ```
*   **List Literals**: Constructed using cons cells. They can be regular lists (ending with `()`) or dotted lists (ending with any non-`()` value).

    ```lisp
    (a b c)        ; Regular list ending with ()
    (a . b)        ; Dotted list ending with b
    (a b . c)      ; Dotted list ending with c
    ```

### List Operators

**UniotLisp** provides fundamental list manipulation operators: `cons`, `car`, `cdr`, and `setcar`.

*   **`cons`**: Constructs a cons cell from two arguments, setting the first argument as the `car` and the second as the `cdr`.

    ```lisp
    (cons 'a 'b)   ; -> (a . b)
    (cons 'a '(b)) ; -> (a b)
    ```
*   **`car`**: Retrieves the first element (`car`) of a cons cell.

    ```lisp
    (car '(a . b)) ; -> a
    (car '(a b c)) ; -> a
    ```
*   **`cdr`**: Retrieves the second element (`cdr`) of a cons cell.

    ```lisp
    (cdr '(a . b)) ; -> b
    (cdr '(a b c)) ; -> (b c)
    ```
*   **`setcar`**: Mutates the `car` of an existing cons cell. It takes two arguments: the cons cell to mutate and the new value for the `car`.

    ```lisp
    (define cell (cons 'a 'b))
    cell          ; -> (a . b)
    (setcar cell 'x)
    cell          ; -> (x . b)
    ```

### Numeric Operators

**UniotLisp** includes basic arithmetic and comparison operators: `+`, `-`, `*`, `/`, `%`, `<`, `<=`, `>`, `>=`, `=`, and `abs`.

*   **`+`**: Returns the sum of its arguments.

    ```lisp
    (+ 1)      ; -> 1
    (+ 1 2)    ; -> 3
    (+ 1 2 3)  ; -> 6
    ```
*   **`-`**: Negates its argument if only one argument is provided; otherwise, subtracts each subsequent argument from the first.

    ```lisp
    (- 3)      ; -> -3
    (- -5)     ; -> 5
    (- 5 2)    ; -> 3
    (- 5 2 7)  ; -> -4
    ```
*   **`*`**: Returns the product of its arguments.

    ```lisp
    (* 2 3 4)  ; -> 24
    ```
*   **`/`**: Divides the first argument by the subsequent arguments. Raises an error on division by zero.

    ```lisp
    (/ 20 4)  ; -> 5
    (/ 10 0)  ; Error: Division by zero
    ```
*   **`%`**: Computes the modulo of the first argument by the second. Raises an error on division by zero.

    ```lisp
    (% 10 3) ; -> 1
    (% 10 0) ; Error: Division by zero
    ```
*   **`<`**: Checks if the first argument is less than the second. Returns `#t` if true, otherwise `()`.

    ```lisp
    (< 2 3)    ; -> #t
    (< 3 3)    ; -> ()
    (< 4 3)    ; -> ()
    ```
*   **`<=`**: Checks if the first argument is less than or equal to the second. Returns `#t` if true, otherwise `()`.

    ```lisp
    (<= 2 3)   ; -> #t
    (<= 3 3)   ; -> #t
    (<= 4 3)   ; -> ()
    ```
*   **`>`**: Checks if the first argument is greater than the second. Returns `#t` if true, otherwise `()`.

    ```lisp
    (> 3 2)    ; -> #t
    (> 3 3)    ; -> ()
    (> 2 3)    ; -> ()
    ```
*   **`>=`**: Checks if the first argument is greater than or equal to the second. Returns `#t` if true, otherwise `()`.

    ```lisp
    (>= 3 2)   ; -> #t
    (>= 3 3)   ; -> #t
    (>= 2 3)   ; -> ()
    ```
*   **`=`**: Checks if two integers or boolean values are equal. Returns `#t` if both arguments are the same integer or both represent the same boolean value, otherwise returns `()`.

    ```lisp
    (= 11 11)  ; -> #t
    (= 11 6)   ; -> ()
    (= #t #t)  ; -> #t
    (= #t ())  ; -> ()
    (= #t 1)   ; -> #t
    (= #t 0)   ; -> ()
    (= () 0)   ; -> #t
    (= () 1)   ; -> ()
    ```
*   **`abs`**: Computes the absolute value of an integer.

    ```lisp
    (abs -5) ; -> 5
    ```

### Logical Operations

**UniotLisp** provides logical operations for boolean expressions: `and`, `or`, and `not`.

*   **`and`**: Returns `#t` if all arguments are true; otherwise, returns `()`.

    ```lisp
    (and (> 5 3) (< 2 4)) ; -> #t
    (and (> 5 3) (< 2 1)) ; -> ()
    ```
*   **`or`**: Returns `#t` if any argument is true; otherwise, returns `()`.

    ```lisp
    (or (> 5 3) (< 2 1))  ; -> #t
    (or (< 5 3) (< 2 1))  ; -> ()
    ```
*   **`not`**: Returns `#t` if the argument is `()`, otherwise returns `()`.

    ```lisp
    (not #t) ; -> ()
    (not ()) ; -> #t
    ```

### Conditionals

**UniotLisp** provides the `if` special form for conditional execution and `eq` for testing equivalence between objects.

* **`(if condition then-expr else-expr)`**:
  * **Behavior**: Evaluates `condition`. If the result is a true value (`#t` or any non-`()` value), it evaluates and returns `then-expr`. Otherwise, it evaluates and returns `else-expr`.
  *   **Examples**:

      ```lisp
      (if (> 3 2) 'yes 'no) ; -> yes
      (if (< 1 0) 'positive 'negative) ; -> negative
      ```
* **`eq`**:
  * **Behavior**: Performs a pointer comparison. Returns `#t` if both arguments reference the exact same object, otherwise returns `()`.
  *   **Examples**:

      ```lisp
      (eq 'a 'a) ; -> #t
      (eq '(1) '(1)) ; -> ()
      (define x (cons 'a 'b))
      (eq x x) ; -> #t
      (eq (cons 'a 'b) x) ; -> ()
      ```

### Loops

**UniotLisp** supports looping through the `while` special form.

*   **Syntax**:

    ```lisp
    (while condition expr ...)
    ```
* **Behavior**: Continues to evaluate `expr ...` as long as `condition` evaluates to a true value (`#t` or any non-`()` value). The loop terminates when `condition` evaluates to `()`.
*   **Example**:

    ```lisp
    (define counter 0)
    (while (< counter 5)
      (print counter)
      (setq counter (+ counter 1)))
    ```

    **Output**:

    ```
    0
    1
    2
    3
    4
    ```
* **Note**: Unlike Scheme, **UniotLisp** does not support tail recursion for loops. Tail calls consume stack space, leading to memory exhaustion errors if used for looping.

### Quoting and Evaluation

**UniotLisp** provides mechanisms to control the evaluation of expressions and manipulate code as data. This section covers the `quote` special form, the shorthand single quote (`'`), the `eval` primitive, and the `list` primitive.

* **`quote`**: The `quote` special form is used to prevent the evaluation of an expression. Instead of evaluating its argument, `quote` returns the expression itself as data.
  *   **Syntax**:

      ```lisp
      (quote expression)
      ```
  * **Behavior**:
    * Returns the `expression` without evaluating it.
    * Useful for representing literal data structures or symbols.
  *   **Examples**:

      ```lisp
      (quote (a b c)) ; -> (a b c)
      (quote 42)      ; -> 42
      (quote x)       ; -> x
      ```
* **`'`** (Single Quote): The single quote (`'`) is a shorthand notation for the `quote` special form, providing a more concise way to prevent evaluation of an expression.
  *   **Syntax**:

      ```lisp
      'expression
      ```
  * **Behavior**:
    * Equivalent to `(quote expression)`.
    * Enhances readability and reduces verbosity in code.
  *   **Examples**:

      ```lisp
      '(a b c) ; Equivalent to (quote (a b c))
      '42      ; Equivalent to (quote 42)
      'x       ; Equivalent to (quote x)
      ```
* **`eval`**: The `eval` primitive evaluates a given expression within the current environment. It takes a quoted expression and returns the result of its evaluation.
  *   **Syntax**:

      ```lisp
      (eval expression)
      ```
  * **Behavior**:
    * Evaluates the `expression` as if it were entered directly.
    * Useful for dynamic code execution and metaprogramming.
  *   **Examples**:

      ```lisp
      (eval '(+ 1 2)) ; -> 3
      (eval '(* 3 4)) ; -> 12
      (define a 10)
      (eval '(+ a 5)) ; -> 15
      ```
  * **Notes**:
    * The argument to `eval` must be a quoted expression; otherwise, it will be evaluated before being passed to `eval`.
    * Use `eval` with caution, as it can execute arbitrary code, which may lead to security vulnerabilities if not managed properly.
* **`list`**: The `list` primitive constructs a new list from its evaluated arguments. It takes any number of arguments, evaluates each one, and returns a list containing those values.
  *   **Syntax**:

      ```lisp
      (list expr1 expr2 ...)
      ```
  * **Behavior**:
    * Evaluates each `expr` and assembles them into a new list.
    * Useful for creating dynamic lists based on runtime values.
  *   **Examples**:

      ```lisp
      (list 1 2 3)          ; -> (1 2 3)
      (list 'a 'b 'c)       ; -> (a b c)
      (list (+ 1 2) (* 3 4)) ; -> (3 12)
      ```
  * **Notes**:
    * Unlike `quote`, the arguments to `list` are evaluated before being included in the new list.
    * Combining `list` with `quote` allows for flexible construction of complex data structures.

### Output Operators

**UniotLisp** provides the `print` primitive for outputting objects to the standard output.

* **`print`**:
  * **Purpose**: Prints the string representation of a given object.
  *   **Usage**:

      ```lisp
      (print 3)               ; Prints "3"
      (print '(hello world))  ; Prints "(hello world)"
      (print #t)              ; Prints "#t"
      (print ())              ; Prints "()"
      ```
  * **Behavior**: Outputs the evaluated object to the standard output. Does not return the printed object; instead, it returns `()`.

### Definitions

**UniotLisp** supports defining variables and functions using `define`, `setq`, `lambda`, and `defun`.

* **Defining Variables**:
  *   **Syntax**:

      ```lisp
      (define variable-name expression)
      ```
  * **Behavior**: Evaluates `expression` and binds the result to `variable-name` in the current environment.
  *   **Example**:

      ```lisp
      (define a (+ 1 2)) ; a is now 3
      (+ a a)             ; -> 6
      ```
* **Assigning Values to Variables**
  *   **Syntax**:

      ```lisp
      (setq variable-name expression)
      ```
  * **Behavior**: Updates the binding of the variable with the evaluated expression. Raises an error if the variable is not defined.
  *   **Example**:

      ```lisp
      (define val (+ 3 5))  ; val is now 8
      (setq val (+ val 1))  ; val is now 9
      ```
*   **Defining Functions**:

    There are two primary ways to define functions in **UniotLisp**: using `lambda` and `defun`.

    * **Using `lambda`**:
      *   **Syntax**:

          ```lisp
          (lambda (arg1 arg2 ...) body ...)
          ```
      * **Behavior**: Creates an anonymous function that can be assigned to a variable or used directly.
      *   **Example**:

          ```lisp
          (define double (lambda (x) (+ x x))) ; Defines a function 'double'
          (double 6)                           ; -> 12
          ((lambda (x) (+ x x)) 6)             ; -> 12
          ```
    * **Using `defun`**:
      *   **Syntax**:

          ```lisp
          (defun function-name (arg1 arg2 ...) body ...)
          ```
      * **Behavior**: Defines a named function, equivalent to using `define` with `lambda`.
      *   **Example**:

          ```lisp
          (defun double (x) (+ x x))  ; Defines a function 'double'
          (double 6)                  ; -> 12
          ```
      *   **Note**:

          You can write a function that takes a variable number of arguments. If the parameter list is a dotted list, the remaining arguments are bound to the last parameter as a list.

          ```lisp
          (defun fn (expr . rest) rest)
          (fn 1)     ; -> ()
          (fn 1 2 3) ; -> (2 3)
          ```
*   **Variable Scope and Lexical Binding**:

    Variables in **UniotLisp** are **lexically scoped** and have indefinite extent. This means that references to "outer" variables remain valid even after the function that created the variables returns.

    **Example**:

    ```lisp
    ;; Define a function that creates a new counter
    (define make-counter
      (lambda ()
        (define count 0)           ; Initialize 'count' to 0
        (lambda ()
          (setq count (+ count 1)) ; Increment 'count' by 1
          count)))                 ; Return the updated 'count'

    ;; Create two independent counters
    (define counter-a (make-counter)) ; Counter A starts at 0
    (define counter-b (make-counter)) ; Counter B starts at 0

    ;; Using Counter A
    (counter-a) ; -> 1
    (counter-a) ; -> 2
    (counter-a) ; -> 3

    ;; Using Counter B
    (counter-b) ; -> 1
    (counter-b) ; -> 2

    ;; Demonstrates lexical scoping
    ;; Define a new scope with a local variable 'count'
    (define manipulate-counter
      (lambda ()
        (define count 100)        ; Local 'count' in this scope
        (counter-a)               ; Call Counter A
        count))                   ; Return local 'count'

    ;; Call manipulate-counter
    ;; The returned value is 100, but the incremented value of
    ;; Counter A is 4. The local 'count' does not interfere with
    ;; Counter A's 'count'.
    (manipulate-counter) ; -> 100
    ;; Call Counter A again
    (counter-a) ; -> 5
    ;; Call Counter B again
    (counter-b) ; -> 3
    ```

### Macros

Macros in **UniotLisp** provide powerful metaprogramming capabilities by allowing code transformations before evaluation.

* **Defining Macros (`defmacro`)**:
  *   **Syntax**:

      ```lisp
      (defmacro macro-name (arg1 arg2 ...) body ...)
      ```
  * **Behavior**: Defines a macro that takes expressions as input and returns a new expression to be evaluated.
  *   **Example**: Define an `unless` macro that acts as the opposite of `if`.

      ```lisp
      (defmacro unless (condition expr)
        (list 'if condition () expr))
      ```
* **Macro Expansion**:
  * **Purpose**: Transforms macro calls into their expanded forms before evaluation.
  *   **Example Usage**:

      ```lisp
      (define x 0)
      (unless (= x 0) '(x is not 0))  ; -> ()
      (unless (= x 1) '(x is not 1))  ; -> (x is not 1)
      ```
* **`macroexpand`**:
  * **Purpose**: A special form to view the expanded form of a macro without evaluating it.
  *   **Syntax**:

      ```lisp
      (macroexpand macro-call)
      ```
  *   **Example**:

      ```lisp
      (macroexpand (unless (= x 1) '(x is not 1)))
      ;; -> (if (= x 1) () (quote (x is not 1)))
      ```
* **`gensym`**:
  * **Purpose**: Generates a unique symbol that is guaranteed not to be `eq` to any other symbol except itself. Useful for creating unique identifiers within macros.
  *   **Usage**:

      ```lisp
      (gensym) ; -> G__0, G__1, etc.
      ```

### Comments

Comments in **UniotLisp** follow the traditional Lisp syntax, using the semicolon (`;`) to start a single-line comment.

*   **Syntax**:

    ```lisp
    ; This is a single-line comment
    ```
* **Behavior**: The interpreter ignores any text following a semicolon until the end of the line.
*   **Example**:

    ```lisp
    (define a 10) ; This defines variable 'a' with value 10
    (+ a 5)       ; -> 15
    ```



For further assistance or to contribute to the project, please refer to the project's repository or contact the maintainers.
