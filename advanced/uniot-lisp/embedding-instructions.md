# Embedding Instructions

This page is for C and C++ developers who want to run the UniotLisp interpreter inside their own program: create it, give it functions of their own, and evaluate code with it.

{% hint style="info" %}
If you are writing firmware with [Uniot Core](../uniot-core.md), you don't need this page. Uniot Core creates and runs the interpreter for you, and adds functions to it through a higher-level API — see [Primitives](../../general-concepts/primitives.md).
{% endhint %}

The interpreter is a single C file with no dependencies beyond the C standard library. It allocates one heap when it starts and never calls `malloc` again, which is what makes it suitable for microcontrollers.

## Getting the source

The source is in the [uniot-lisp](https://github.com/uniot-io/uniot-lisp) repository: `src/libminilisp.c` and `src/libminilisp.h`. With PlatformIO, add it to your project by version tag:

```ini
lib_deps =
    https://github.com/uniot-io/uniot-lisp.git#0.4.0
```

In any other build, compile `libminilisp.c` along with your own sources and include `libminilisp.h`.

## A minimal host

This complete program creates an interpreter, evaluates an expression, and prints the result:

```c
#include <stdio.h>
#include "libminilisp.h"

static void print_out(const char *msg, int size) { printf("%.*s\n", size, msg); }
static void print_log(const char *msg, int size) { printf("log: %.*s\n", size, msg); }
static void print_err(const char *msg, int size) { fprintf(stderr, "error: %.*s\n", size, msg); }

int main(void) {
    void *root = NULL;
    DEFINE1(env);

    lisp_set_printers(print_out, print_log, print_err);

    lisp_create(24576, 8192);   // a 24 KB heap, 8 KB of stack for evaluation
    if (!lisp_is_created()) {
        return 1;
    }

    *env = make_env(root, &Nil, &Nil);
    define_constants(root, env);
    define_primitives(root, env);

    lisp_eval(root, env, "(+ 1 2)");   // prints 3

    lisp_destroy();
    return 0;
}
```

Step by step:

1. **`root` and `DEFINE1(env)`** set up the garbage collector's view of your variables — see [Keeping objects alive](#keeping-objects-alive). The environment holds every definition, so it must be one of them.
2. **`lisp_set_printers`** installs the functions that receive output — see [Output and errors](#output-and-errors).
3. **`lisp_create`** allocates the heap. Check **`lisp_is_created`** afterwards: a heap that can't be allocated, or is larger than the interpreter can address, leaves it false.
4. **`make_env`** creates the global environment, and **`define_constants`** and **`define_primitives`** fill it with the language's built-in values and functions.
5. **`lisp_eval`** reads and evaluates a string of code.
6. **`lisp_destroy`** frees the heap. Call `lisp_create` again to start over.

When the environment must outlive the function that creates it — in firmware, where it is created in `setup()` and used in every later call — declare the root frame at file scope instead, as the interpreter's own REPL does:

```c
static void *root = NULL;
static void *root_frame[3];
static Obj **env;

void setup_interpreter(void) {
    root_frame[0] = root;
    root_frame[1] = NULL;
    root_frame[2] = ROOT_END;
    root = root_frame;
    env = (Obj **)(root_frame + 1);
    // ... then lisp_create, make_env and the rest as above
}
```

## Heap and stack

```c
void lisp_create(size_t size, size_t max_eval_stack);
```

**`size`** is the heap, in bytes. Every value a script creates lives in it. The largest heap that can be asked for is `LISP_MAX_HEAP`, 65535 bytes; `lisp_create` refuses anything larger. **`lisp_mem_used()`** returns how much of the heap is in use.

**`max_eval_stack`** limits how much of the C stack a single evaluation may use, in bytes. Recursion in a script runs on the C stack, and overrunning it would crash the whole program, so the interpreter measures what it uses as it goes and stops the script with an error before that happens. Pass `0` to remove the limit.

To choose a value, start from the stack available where you call `lisp_eval`, subtract what your error handling needs, and leave a margin. The global **`eval_stack_max`** records the most stack any evaluation has used since `lisp_create`; run your heaviest scripts and read it.

For reference, Uniot Core gives scripts a 24 KB heap and 3 KB of evaluation stack on an ESP32, and 12 KB and 1.25 KB on an ESP8266.

## Evaluating code

| Function | What it does |
| --- | --- |
| `bool lisp_eval(void *root, Obj **env, const char *code)` | Reads and evaluates every expression in `code`, in order. Returns `false` if one of them failed, and stops there. |
| `bool safe_eval(void *root, Obj **env, Obj **expr)` | Evaluates one expression that has already been read. Returns `false` if it failed. |
| `Obj *eval(void *root, Obj **env, Obj **obj)` | Evaluates one expression, raising errors to the caller — for use inside [primitives](#adding-primitives). |
| `Obj *eval_list(void *root, Obj **env, Obj **list)` | Evaluates each element of a list and returns a list of the results. |

The value of each expression is passed to the output printer.

## Output and errors

```c
typedef void (*print_def)(const char *msg, int size);
void lisp_set_printers(print_def out, print_def log, print_def err);
```

The interpreter never writes anywhere itself. It hands text to three functions you provide:

| Printer | Receives |
| --- | --- |
| `out` | The value of each expression `lisp_eval` evaluates |
| `log` | What the script prints with `print` |
| `err` | The message of an error that stopped the script |

The text is not null-terminated; use `size`. Two rules apply to every printer, and neither is checked:

- **Copy the text before returning.** It lives in a buffer the interpreter reuses.
- **Don't evaluate Lisp from inside a printer**, directly or indirectly. The error printer in particular runs partway through the interpreter recovering from the error.

When `lisp_eval` returns `false`, **`lisp_error_idx()`** and **`lisp_error_end()`** give the span of the expression that failed, as offsets into the code you passed — enough to highlight it in an editor:

```c
const char *code = "(+ 1 2)\n(foo 3)\n(+ 4 5)";
if (!lisp_eval(root, env, code)) {
    int start = lisp_error_idx();   // 8
    int end = lisp_error_end();     // 15: the span is "(foo 3)"
}
```

Here the first expression prints `3`, the second fails with `Undefined symbol: foo`, and the third is never evaluated.

## Adding primitives

A primitive is a function written in C that a script can call by name. This is how a host gives scripts access to its hardware or services.

```c
typedef struct Obj *Primitive(void *root, struct Obj **env, struct Obj **args);
```

A primitive receives its arguments **unevaluated**, as a list. It decides whether and how to evaluate them — usually all of them, with `eval_list`. It returns a value, and reports a problem by calling `error()`, which stops the script and never returns.

This one adds two integers:

```c
static Obj *prim_add_two(void *root, Obj **env, Obj **args) {
    if (length(*args) != 2)
        error("add-two takes two arguments");

    Obj *values = eval_list(root, env, args);
    Obj *a = values->car;
    Obj *b = values->cdr->car;
    if (a->type != TINT || b->type != TINT)
        error("add-two takes only numbers");

    int32_t sum;
    if (__builtin_add_overflow(a->value, b->value, &sum))
        error("Integer overflow in add-two");
    return make_int(root, sum);
}
```

Register it after `define_primitives`, under the name scripts will use:

```c
add_primitive(root, env, "add-two", prim_add_two);
```

```lisp
(add-two 3 4)     ; -> 7
(add-two 3)       ; -> error: add-two takes two arguments
(add-two 'a 4)    ; -> error: add-two takes only numbers
```

The pieces a primitive works with:

| | |
| --- | --- |
| `int length(Obj *list)` | The number of elements, or `-1` if it isn't a proper list |
| `Obj *make_int(void *root, int32_t value)` | A new integer |
| `Obj *make_symbol(void *root, const char *name)` | A new symbol |
| `True`, `Nil` | The values `#t` and `()`, to return as truth values |
| `obj->type` | One of `TINT`, `TCELL`, `TSYMBOL`, `TPRIMITIVE`, `TFUNCTION`, `TMACRO`, `TENV`, `TTRUE`, `TNIL` |
| `obj->value` | The number, when `type` is `TINT` |
| `obj->car`, `obj->cdr` | The two halves, when `type` is `TCELL` |
| `obj->name` | The name, when `type` is `TSYMBOL` |
| `error(fmt, ...)` | Stops the script with a `printf`-style message |

Integer arithmetic in the language raises on overflow, and a primitive that does its own arithmetic should do the same, as `add-two` does.

### Keeping objects alive

The garbage collector reclaims every object it can't find a reference to, and it can run whenever anything is allocated — inside `make_int`, `eval_list`, or any other call that creates a value. A pointer held only in an ordinary C variable is invisible to it, so an object you still need can be reclaimed while you hold it.

`add-two` is safe without extra care because it reads both numbers out of the list before its one allocation, `make_int`. A primitive that has to keep an object across an allocation must declare it with one of the **`DEFINE1`** to **`DEFINE7`** macros, which make it visible to the collector.

This one evaluates its two arguments one at a time and returns the first. It holds the first result while it evaluates the second, which can allocate, so the first must be declared:

```c
static Obj *prim_first_of(void *root, Obj **env, Obj **args) {
    if (length(*args) != 2)
        error("first-of takes two arguments");

    DEFINE1(first);
    *first = eval(root, env, &(*args)->car);
    eval(root, env, &(*args)->cdr->car);   // may collect; *first survives because it is declared
    return *first;
}
```

```lisp
(first-of (list 1 2) (list 3 4))   ; -> (1 2)
```

The macros declare `Obj **` variables, so use them through `*`. Declare them before any loop, never inside one.

## Adding constants

A constant is a name with a fixed value. Scripts can read it but not change it.

```c
add_constant_int(root, env, "LED_COUNT", 10);

DEFINE1(greeting);
*greeting = make_symbol(root, "hello");
add_constant(root, env, "GREETING", greeting);
```

```lisp
LED_COUNT            ; -> 10
(setq LED_COUNT 5)   ; -> error: Cannot change constant LED_COUNT
```

**`get_variable(root, env, name)`** looks a name up from C — to read a value a script has set, for example. It raises if the name isn't defined.

## Declaring functions the host implements elsewhere

**`handle_pruner`** is for a host that implements some functions somewhere other than C — in JavaScript in a browser, say — and wants a script to declare them in Lisp. Call it from a primitive that acts as a declaration form, passing the name of a single dispatch primitive:

```c
static Obj *prim_defjs(void *root, Obj **env, Obj **args) {
    return handle_pruner(root, env, args, "js_call", true);
}
```

```lisp
(defjs vibro (times))
```

This defines `vibro` as a function of one argument whose body calls `(js_call 'vibro times)`. With `include_name` false, the name is left out and the body is `(js_call times)`. Declaring a name that is already defined is an error.

## Letting other work run

```c
typedef void (*yield_def)();
void lisp_set_cycle_yield(yield_def yield);
```

A script's loop can run for a long time without returning control. Set a yield function and the interpreter calls it on every `while` iteration and every tail call, so the host can feed a watchdog timer or let other tasks run.

A script that loops forever is stopped with an error rather than hanging the host — see [Build configuration](#build-configuration).

## Garbage collection

The collector is chosen when the library is compiled:

| `MINILISP_GC` | |
| --- | --- |
| `MINILISP_GC_MARK_SWEEP` (default) | Objects never move, and collecting needs no memory beyond the heap. Suits small devices, where a second heap-sized block may not be available. |
| `MINILISP_GC_COPYING` | Allocation is faster, but every collection needs a second block the size of the heap, and objects move. |

Mark-sweep is the default everywhere on purpose: the two collectors run out of memory under different conditions, so the same script could fit on one and fail on the other.

**`gc(root)`** runs a collection immediately. Setting **`always_gc`** to `true` runs one before every allocation, which makes a primitive that forgets to [keep an object alive](#keeping-objects-alive) fail at once instead of occasionally.

## Build configuration

These are compile-time definitions; set them with `-D` to override the default.

| Definition | Default | Effect |
| --- | --- | --- |
| `MINILISP_MAX_LOOP_ITERATIONS` | 20000 | `while` iterations allowed in one top-level expression, counted across all its loops, before it is stopped as endless |
| `MINILISP_MAX_TAIL_CALLS` | same | Tail calls allowed in one chain before it is stopped as endless |
| `MINILISP_GC` | `MINILISP_GC_MARK_SWEEP` | The collector, as above |
| `MINILISP_GC_MARK_STACK` | 128 | The mark-sweep collector's work stack, in entries. Running out is not an error, only slower. |
| `MINILISP_GC_DEBUG` | 0 | `1` adds `debug_gc` (log each collection), `verify_gc` (check the heap after each) and `fail_gc_alloc` (simulate running out of memory) — for debugging a collector or a primitive |
| `MINILISP_GC_STATS` | 0 | `1` adds the `lisp_stats` counters and `lisp_stats_reset()` for measuring collector performance, timed by a clock you assign to `lisp_stats_clock` |

These are fixed in the header:

| Limit | Value |
| --- | --- |
| `LISP_MAX_HEAP` | 65535 — the largest heap |
| `SYMBOL_MAX_LEN` | 64 — the longest symbol name |
| `LISP_MESSAGE_MAX_LEN` | 128 — the longest error or log message |
| `LISP_PRINT_MAX_LEN` | 256 — the longest printed value; output is truncated to it |

`LISP_VERSION` holds the library version as a single integer: `major * 10000 + minor * 100 + patch`, so 0.4.0 is `400`.
