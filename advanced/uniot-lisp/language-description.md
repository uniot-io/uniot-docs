# Language Description

This page describes the UniotLisp language itself: its values, its forms, and how they behave. It is for anyone writing UniotLisp by hand, or wanting to understand the code the [Visual Editor](../../platform/sandbox/visual-editor/) generates.

What a script can do on a device — run tasks, exchange events, read and drive pins — comes from functions the device provides. Those are covered in [Scripting](../../general-concepts/scripting.md) and [Primitives](../../general-concepts/primitives.md).

## Reading the examples

UniotLisp reads one expression at a time, evaluates it, and returns a value. In the examples, `; ->` shows what an expression evaluates to:

```lisp
(+ 1 2)   ; -> 3
```

When an expression stops with an error instead, the example says so:

```lisp
(/ 7 0)   ; -> error: Division by zero
```

## Values

### Integers

Integers are 32-bit and signed. Arithmetic that would overflow stops with an error rather than wrapping around, and a number too large to represent is refused when the script is read.

```lisp
42                ; -> 42
-7                ; -> -7
(* 2000000000 2)  ; -> error: Integer overflow in *
```

There are no floating-point numbers. To work with fractions, scale your values — hundredths of a degree instead of degrees, for example.

### Truth: `()` and `#t`

`()` is the only false value. It is also the empty list.

`#t` is the true literal, but **any value other than `()` is true — including `0`**:

```lisp
(if () 'yes 'no)   ; -> no
(if 0 'yes 'no)    ; -> yes
(if #t 'yes 'no)   ; -> yes
```

This matters on a device, where a pin read or an event value arrives as a number, and `0` is a true value like any other. To treat `0` as false, use [`bool`](#truth-and-predicates).

### Symbols

Symbols are names, such as `x`, `counter` or `my-function`. Two symbols with the same name are the same object. UniotLisp has no string type, so symbols often stand in for text:

```lisp
'hello   ; -> hello
```

### Lists

Lists are built from cons cells: pairs of two values. A proper list ends in `()`; a dotted list ends in any other value.

```lisp
'(a b c)     ; -> (a b c)
'(a . b)     ; -> (a . b)
'(a b . c)   ; -> (a b . c)
```

## Quoting and evaluation

A symbol is evaluated to the value it names, and a list to the result of calling its first element. **`quote`** prevents that, returning its argument as data. The single quote `'` is shorthand for it.

```lisp
(quote (a b c))   ; -> (a b c)
'(a b c)          ; -> (a b c)
'x                ; -> x
```

**`eval`** does the opposite: it evaluates data as code.

```lisp
(eval '(+ 1 2))   ; -> 3
(define a 10)
(eval '(+ a 5))   ; -> 15
```

**`list`** builds a list from its arguments, which — unlike with `quote` — are evaluated first:

```lisp
(list 1 2 3)             ; -> (1 2 3)
(list (+ 1 2) (* 3 4))   ; -> (3 12)
```

## Lists

| Function | What it does |
| --- | --- |
| `(cons a b)` | A new pair with `a` first and `b` second |
| `(car list)` | The first element |
| `(cdr list)` | Everything after the first element |
| `(setcar pair value)` | Replaces the first element of a pair |
| `(setcdr pair value)` | Replaces the rest of a pair |
| `(length list)` | The number of elements |
| `(list a b ...)` | A list of its arguments |
| `(apply function list)` | Calls a function with the elements of a list as its arguments |

```lisp
(cons 'a 'b)             ; -> (a . b)
(cons 'a '(b))           ; -> (a b)
(car '(a b))             ; -> a
(cdr '(a b))             ; -> (b)
(length '(1 2))          ; -> 2
(apply + (list 1 2 3))   ; -> 6
```

`car` and `cdr` of `()` are `()`, so walking off the end of a list is not an error:

```lisp
(car ())   ; -> ()
(cdr ())   ; -> ()
```

## Arithmetic

`+`, `-`, `*`, `/` and `%` take any number of arguments; `abs` gives the magnitude of a number.

```lisp
(+ 1 2 3)   ; -> 6
(- 3)       ; -> -3
(- 5 2 7)   ; -> -4
(* 2 3 4)   ; -> 24
(abs -5)    ; -> 5
(+)         ; -> 0
(*)         ; -> 1
```

`/` and `%` are integer operations that truncate towards zero:

```lisp
(/ 7 2)    ; -> 3
(/ -7 2)   ; -> -3
(% 10 3)   ; -> 1
(% -7 2)   ; -> -1
```

Division by zero and overflow both stop the script with an error.

## Comparison

`<`, `<=`, `>` and `>=` compare numbers. Given more than two arguments, they check every neighbouring pair:

```lisp
(< 2 3)     ; -> #t
(< 3 3)     ; -> ()
(<= 3 3)    ; -> #t
(< 1 2 3)   ; -> #t
(< 1 3 2)   ; -> ()
```

**`eql`** is equality. Numbers are equal when their values are; everything else only when it is the very same object. Two lists with the same contents are not `eql`, because they are two different lists.

```lisp
(eql 1 1)                 ; -> #t
(eql 'a 'a)               ; -> #t
(eql (list 1) (list 1))   ; -> ()
```

**`=`** compares numbers, and also compares a number with a truth value by treating any non-zero number as true. That makes it convenient for testing a flag — but it is not an equality, so use `eql` when you mean "the same".

```lisp
(= 11 11)   ; -> #t
(= 1 #t)    ; -> #t
(= 0 ())    ; -> #t
```

## Truth and predicates

These ask what kind of value something is:

| Predicate | True when the value is |
| --- | --- |
| `numberp` | a number |
| `symbolp` | a symbol |
| `consp` | a pair — a non-empty list |
| `listp` | a list, including `()` |
| `atom` | anything but a pair, including `()` |
| `functionp` | a function |

```lisp
(numberp 1)       ; -> #t
(consp '(a))      ; -> #t
(atom 'a)         ; -> #t
(listp ())        ; -> #t
(functionp car)   ; -> #t
```

**`not`** inverts truth under the language's own rule, where only `()` is false:

```lisp
(not ())   ; -> #t
(not 0)    ; -> ()
```

**`bool`** converts a value to `#t` or `()` under the *numeric* rule instead: `0` and `()` are false, everything else is true. It exists for device values — a pin read or an event value carries its truth as `0` or `1`, and `not` on one of those asks the wrong question.

```lisp
(bool 0)    ; -> ()
(bool 1)    ; -> #t
(bool ())   ; -> ()
(bool 'a)   ; -> #t
```

`bool` never fails, whatever it is given, and applying it to a value that is already `#t` or `()` changes nothing. If a script uses it often, give it a shorter name — `?` is a valid symbol:

```lisp
(define ? bool)
(? 0)   ; -> ()
```

## Conditionals and sequencing

**`if`** takes a condition, an expression to evaluate when it is true, and optionally one for when it is false:

```lisp
(if (< 1 2) 'smaller 'larger)   ; -> smaller
(if () 'yes)                    ; -> ()
```

**`progn`** evaluates several expressions in order and returns the last one's value — the way to do more than one thing where a single expression is expected:

```lisp
(progn 1 2 3)   ; -> 3
```

**`and`** and **`or`** stop as soon as the answer is known, and return the value that decided it:

```lisp
(and 1 2)    ; -> 2
(and 1 ())   ; -> ()
(or () 5)    ; -> 5
(and)        ; -> #t
(or)         ; -> ()
```

Because `and` stops at the first false value, it can guard an expression that would otherwise fail — such as `(and (consp x) (car x))`.

## Loops and recursion

**`while`** repeats its body as long as its condition is true. Inside the loop, `#itr` is the number of the current iteration, counting from zero; in nested loops it belongs to the innermost one.

```lisp
(define total 0)
(while (< #itr 3) (setq total (+ total 1)))
total   ; -> 3
```

On a device, a script usually doesn't loop forever itself. It runs its work in a [task](../../general-concepts/scripting.md), which the device repeats on a schedule. A loop that never ends is stopped with an error rather than hanging the device.

**A call in tail position uses no extra memory**, so a function that calls itself as the last thing it does runs in constant space, however long the list. This is the usual way to walk a list:

```lisp
(defun sum (l acc)
  (if (eql l ()) acc (sum (cdr l) (+ acc (car l)))))
(sum '(1 2 3) 0)   ; -> 6
```

Recursion that is *not* in tail position does use memory with each call, and is limited by the space the device sets aside for evaluation. Write recursive functions with an accumulator, as `sum` does, and they won't reach that limit.

## Definitions

| Form | What it does |
| --- | --- |
| `(define name value)` | Binds a variable |
| `(defun name (params ...) body ...)` | Defines a function |
| `(lambda (params ...) body ...)` | Makes a function without a name |
| `(setq name value)` | Assigns to a variable that already exists |

`define` and `defun` may be used again on the same name to replace it.

```lisp
(define a (+ 1 2))
a                          ; -> 3
(defun double (x) (+ x x))
(double 4)                 ; -> 8
(define triple (lambda (x) (* 3 x)))
(triple 4)                 ; -> 12
```

`setq` only assigns to a variable that already exists:

```lisp
(setq a 5)            ; -> 5
(setq undefined 1)    ; -> error: Undefined symbol: undefined
```

A function must be called with exactly as many arguments as it has parameters, and the parameters must have different names:

```lisp
(double 1 2)            ; -> error: Cannot apply function: too many arguments
(defun f (x x) x)       ; -> error: Duplicate parameter: x
```

A parameter list may end in `. name`, which collects the remaining arguments into a list — or be a single name, which collects all of them:

```lisp
(defun rest-of (a . rest) rest)
(rest-of 1 2 3)          ; -> (2 3)
(defun all-of args args)
(all-of 1 2)             ; -> (1 2)
```

Variables live as long as something still uses them. A function can keep one of its own between calls:

```lisp
(define counter
  ((lambda (count)
     (lambda () (setq count (+ count 1)) count))
   0))
(counter)   ; -> 1
(counter)   ; -> 2
```

## Macros

**`defmacro`** defines a macro: it receives its arguments unevaluated, and returns a form that is evaluated in its place.

```lisp
(defmacro unless (test . body)
  (list 'if test () (cons 'progn body)))
(unless (= 1 1) 'no)    ; -> ()
(unless (= 1 2) 'yes)   ; -> yes
```

**`macroexpand`** shows the form a macro produces. It is a function, so quote what you give it:

```lisp
(macroexpand '(unless (= 1 1) 'no))   ; -> (if (= 1 1) () (progn (quote no)))
```

**`gensym`** returns a new symbol that no other code can name, for macros that need a variable of their own.

## Output

**`print`** writes a value and returns it, so it can sit inside a larger expression:

```lisp
(print 'hello)      ; -> hello
(+ 1 (print 2))     ; -> 3
```

On a device, printed lines go to the device's log; in the Sandbox, they appear in the [Logger](../../platform/sandbox/logger.md) and the [Emulator](../../platform/sandbox/emulator.md). See [Debugging Scripts](../../general-concepts/scripting.md#debugging-scripts).

## Comments

`;` begins a comment that runs to the end of the line.

```lisp
; This whole line is a comment
(+ 1 2) ; so is the rest of this one
```

## Writing your own helpers

UniotLisp deliberately leaves out what can be written in UniotLisp itself: a script pays in memory only for what it defines. Here are common helpers, a few lines each. Copy the ones a script needs.

One rule runs through all of them: **call yourself in tail position.** These versions carry their result along as they go, and run in constant space on a list of any length.

```lisp
(defun reverse (l acc)
  (if (eql l ()) acc (reverse (cdr l) (cons (car l) acc))))

(defun member (x l)
  (if (eql l ()) () (if (eql x (car l)) l (member x (cdr l)))))

(defun nth (n l) (if (= n 0) (car l) (nth (- n 1) (cdr l))))

(defun reduce (f l acc)
  (if (eql l ()) acc (reduce f (cdr l) (f acc (car l)))))

(defun map (f l) (map1 f l ()))
(defun map1 (f l acc)
  (if (eql l ()) (reverse acc ()) (map1 f (cdr l) (cons (f (car l)) acc))))

(defun filter (f l) (filter1 f l ()))
(defun filter1 (f l acc)
  (if (eql l ())
      (reverse acc ())
      (filter1 f (cdr l) (if (f (car l)) (cons (car l) acc) acc))))

(defun min (a b) (if (< a b) a b))
(defun max (a b) (if (> a b) a b))
```

```lisp
(reverse '(1 2 3) ())               ; -> (3 2 1)
(nth 1 '(a b c))                    ; -> b
(reduce + '(1 2 3) 0)               ; -> 6
(map double '(1 2 3))               ; -> (2 4 6)
(filter (lambda (x) (> x 1)) '(1 2 3))   ; -> (2 3)
(max 3 7)                           ; -> 7
```

Control structures are macros:

```lisp
(defmacro when (test . body) (list 'if test (cons 'progn body) ()))

;; cond expands one clause at a time, so it takes any number of them
(defmacro cond (clause . rest)
  (if (eql rest ())
      (list 'if (car clause) (cons 'progn (cdr clause)) ())
      (list 'if (car clause) (cons 'progn (cdr clause)) (cons 'cond rest))))
```

```lisp
(when (< 1 2) 'first 'second)          ; -> second
(cond ((< 5 3) 'less) ((> 5 3) 'more)) ; -> more
```

A local variable is a `lambda` applied where it stands:

```lisp
((lambda (x y) (+ x y)) 1 2)   ; -> 3
```

## Coming from an older version

Scripts written before UniotLisp 0.3.0 may need changes. Those that matter most:

- **`eq` is now `eql`.**
- **Only `()` is false.** `0` is true, so `(not 0)` is `()` — use `bool` for device values.
- **`and` and `or` return the value that decided them**, not always `#t`.
- **Overflow is an error**, and **`/` is exact integer division**.
- **Calling a function with the wrong number of arguments is an error.**
- **`define` and `defun` replace an existing definition** instead of refusing it.

The full list is in the [UniotLisp changelog](https://github.com/uniot-io/uniot-lisp/blob/master/CHANGELOG.md).
