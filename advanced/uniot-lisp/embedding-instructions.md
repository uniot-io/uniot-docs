# Embedding Instructions

This section is tailored for developers who intendextend the functionality of the UniotLisp interpreter and understand the details better. It covers setup, initialization, extending the interpreter with custom primitives or constants, utilizing the API, and handling advanced configurations.

## Getting Started

To begin using UniotLisp, follow these steps:

1.  **Obtain the Source Code**:

    Download or clone the **uniot-lisp** repository from GitHub:

    ```sh
    git clone https://github.com/uniot-io/uniot-lisp.git
    ```

    Ensure you have access to the `libminilisp.h`, `libminilisp.c` and `memcheck.h` files.
2. **Include in Your Project**:
   * Add `libminilisp.c` to your project's source files.
   *   Include the header in your code:

       ```c++
       #include "libminilisp.h"
       ```
3.  **Define Print Functions**:

    ```c++
    void printOut(const char *msg, int size) {
        fprintf(stdout, "OUT: %s\n", msg);
    }

    void printLog(const char *msg, int size) {
        fprintf(stdout, "LOG: %s\n", msg);
    }

    void printErr(const char *msg, int size) {
        fprintf(stderr, "ERR: %s\n", msg);
    }
    ```
4.  **Initialize an Environment**:

    ```c++
    void *env_constructor[3];
    void *root = NULL;
    Obj **genv;

    env_constructor[0] = root;
    env_constructor[1] = NULL;
    env_constructor[2] = ROOT_END;
    root = env_constructor;
    genv = (Obj **)(env_constructor + 1);
    ```
5.  **Initialize the Interpreter and Create an Environment**:

    ```c++
    // Initialize the interpreter with a specified memory size (e.g., 4096 bytes)
    lisp_create(4096);
    lisp_set_printers(printOut, printLog, printErr);

    // Create a global environment and define constants and primitives
    *genv = make_env(root, &Nil, &Nil);
    define_constants(root, genv);
    define_primitives(root, genv);
    ```
6.  **Evaluate Lisp Code**:

    ```c++
    const char *code = "(+ 1 2 3)";
    if (lisp_eval(root, genv, code)) {
        // Evaluation succeeded
    } else {
        // Handle evaluation error
    }
    ```
7.  **Cleanup**:

    ```c++
    lisp_destroy();
    ```
8.  **Full Example Code**:

    ```c++
    #include <stdio.h>
    #include "UniotLisp.h"

    void printOut(const char *msg, int size) {
        fprintf(stdout, "OUT: %s\n", msg);
    }

    void printLog(const char *msg, int size) {
        fprintf(stdout, "LOG: %s\n", msg);
    }

    void printErr(const char *msg, int size) {
        fprintf(stderr, "ERR: %s\n", msg);
    }

    int main() {
        void *env_constructor[3];
        void *root = NULL;
        Obj **genv;

        env_constructor[0] = root;
        env_constructor[1] = NULL;
        env_constructor[2] = ROOT_END;
        root = env_constructor;
        genv = (Obj **)(env_constructor + 1);

        lisp_create(4096);
        lisp_set_printers(printOut, printLog, printErr);

        *genv = make_env(root, &Nil, &Nil);
        define_constants(root, genv);
        define_primitives(root, genv);

        const char *code = "(+ 1 2 3)";
        if (lisp_eval(root, genv, code)) {
            // Evaluation succeeded
        } else {
            // Handle evaluation error
        }

        lisp_destroy();

        return 0;
    }
    ```

    This code evaluates the expression `(+ 1 2 3)`, which results in `6`.

## Basic Concepts

Understanding the foundational concepts of UniotLisp will aid in effectively utilizing and extending the interpreter.

### Object Representation

**UniotLisp** represents all Lisp entities as `Obj` structures. Each `Obj` can represent various data types, such as integers, symbols, lists (cons cells), functions, macros, and more.

#### **Obj Structure**

```c++
typedef struct Obj {
    unsigned char type;      // Type tag
    ...
} Obj;
```

#### **Type Tags**

* `TINT`: Integer
* `TCELL`: Cons cell (pair)
* `TSYMBOL`: Symbol
* `TPRIMITIVE`: Primitive function
* `TFUNCTION`: User-defined function
* `TMACRO`: Macro
* `TENV`: Environment frame
* `TMOVED`: Forwarding pointer (used by GC)
* `TTRUE`, `TNIL`, `TDOT`, `TCPAREN`: Special constants

### Memory Management and Garbage Collection

**UniotLisp** employs a **copying garbage collector** based on Cheney's algorithm to manage memory efficiently.

#### **Copying Garbage Collector**

* **Semispace Allocation**: The heap is divided into two equal halves (`memory` and `from_space`). Objects are copied from the active semispace to the other during garbage collection.
* **Forwarding Pointers**: When an object is moved, a forwarding pointer (`TMOVED` type) is placed in its original location to avoid duplicate copies.
* **Root Management**: Roots are managed through macros (`ADD_ROOT`, `DEFINE1`, etc.) that track pointers on the C stack to ensure live objects are retained.

#### **Allocation Strategy**

* **Memory Allocation (`alloc`)**: Allocates memory for new objects, triggering garbage collection if necessary.
* **Memory Exhaustion**: If memory cannot be allocated even after GC, the interpreter terminates with an error.

### Parsing and Evaluation

**UniotLisp** parses Lisp code using a **recursive-descent parser** and evaluates expressions in an environment model.

#### **Parsing**

* **Tokenization**: The `read_expr` function reads characters, identifies tokens (integers, symbols, parentheses), and constructs corresponding `Obj` structures.
* **Symbol Interning**: Symbols are interned to ensure uniqueness, optimizing symbol comparisons and storage.

#### **Evaluation**

* **Evaluator (`eval`)**: Processes `Obj` structures, handling self-evaluating objects, variable lookups, function applications, and macro expansions.
* **Environment Model**: Variables are stored in environments (`TENV`), allowing for lexical scoping and nested environments.

## Adding New Primitives

Extending UniotLisp with new primitives allows you to introduce custom functionalities tailored to your application's needs. This section guides you through the process of defining and registering new primitive functions.

### Defining a Primitive Function

A primitive function in UniotLisp is a C function that follows a specific signature:

```c++
typedef struct Obj *Primitive(void *root, struct Obj **env, struct Obj **args);
```

**Parameters**:

* `void *root`: Root pointer for garbage collection.
* `struct Obj **env`: Current environment.
* `struct Obj **args`: List of arguments passed to the primitive.

**Return Value**: A pointer to an `Obj` representing the result.

**Example**: Define a primitive that adds two integers.

```c++
static Obj *prim_add_two(void *root, Obj **env, Obj **args) {
    if (length(*args) != 2)
        error("add_two expects exactly two arguments");

    Obj *evaluated_args = eval_list(root, env, args);

    if (evaluated_args->car->type != TINT || evaluated_args->cdr->car->type != TINT)
        error("add_two expects integer arguments");

    int sum = evaluated_args->car->value + evaluated_args->cdr->car->value;
    return make_int(root, sum);
}
```

### Registering the Primitive

After defining the primitive function, you need to register it within the interpreter's environment using `add_primitive`.

**Function Signature**:

```c++
void add_primitive(void *root, Obj **env, const char *name, Primitive *fn);
```

**Parameters**:

* `void *root`: Root pointer for garbage collection.
* `Obj **env`: Current environment.
* `const char *name`: Name of the primitive as it will appear in Lisp.
* `Primitive *fn`: Pointer to the C function implementing the primitive.

**Example**: Register the `add_two` primitive.

```c++
add_primitive(root, env, "add-two", prim_add_two);
```

**Usage in Lisp Code**:

```lisp
(add-two 3 4) ; -> 7
```

## Adding Constants

Defining constants allows you to introduce fixed values that can be referenced within Lisp code. Constants are immutable and cannot be reassigned.

Use `add_constant` or `add_constant_int` to register the constant within the environment.

**Function Signatures**:

```c++
void add_constant(void *root, Obj **env, const char *name, Obj **val);
void add_constant_int(void *root, Obj **env, const char *name, int value);
```

### Registering the Constant

**Example**: Register the `#version` constant.

```c++
Obj *VERSION = make_int(root, 10203); // Represents the version 1.2.3
add_constant(root, env, "#version", &VERSION);
```

or

```c++
add_constant_int(root, env, "#version", 10203);
```

**Usage in Lisp Code**:

```lisp
(define legacy-version 10101) ; Represents the legacy version 1.1.1
(if
 (> #version legacy-version)
 (print 'continue)
 (print 'this_version_is_not_supported))
```

## Error Handling

UniotLisp incorporates robust error handling to ensure the interpreter remains stable and provides informative feedback.

### Error Function

The `error` function is used to report errors and terminate the current evaluation gracefully.

```c++
void __attribute((noreturn)) error(const char *fmt, ...);
```

**Usage**:

```c++
error("Undefined symbol: %s", symbol_name);
```

## Non-Local Exits

UniotLisp uses `setjmp` and `longjmp` to handle errors without crashing the interpreter. When an error occurs, the interpreter jumps back to a safe state, allowing for continued operation or graceful termination.

### Common Error Scenarios

Some common error scenarios encountered during Lisp evaluation include:

*   **Malformed Expressions**: Incorrect syntax or structure.

    ```lisp
    (cons 1) ; Error: cons expects exactly two arguments
    ```
*   **Type Mismatches**: Operations on incompatible types.

    ```lisp
    (+ 'a 2) ; Error: + expects integer arguments
    ```
*   **Undefined Symbols**: Referencing symbols that haven't been defined.

    ```lisp
    (print x) ; Error: Undefined symbol x
    ```
*   **Memory Exhaustion**: Running out of allocated memory.

    ```c++
    error("Memory exhausted");
    ```

## API Usage

UniotLisp provides a set of API functions to interact with the interpreter programmatically. These functions facilitate creating environments, evaluating code, managing memory, and customizing interpreter behavior.

### Lifecycle Management

*   **`lisp_create`**: Initializes the interpreter with a specified memory size.

    ```c++
    void lisp_create(size_t size);
    ```
*   **`lisp_destroy`**: Cleans up and frees allocated memory.

    ```c++
    void lisp_destroy(void);
    ```
*   **`lisp_is_created`**: Checks if the interpreter has been initialized.

    ```c++
    bool lisp_is_created();
    ```

### Evaluation Interface

*   **`lisp_eval`**: Parses and evaluates Lisp code from a string.

    ```c++
    bool lisp_eval(void *root, Obj **env, const char *code);
    ```
*   **`safe_eval`**: Evaluates an expression with error protection.

    ```c++
    bool safe_eval(void *root, Obj **env, Obj **expr);
    ```

### Configuration

*   **`lisp_set_cycle_yield`**: Sets a yield function to allow cooperative multitasking during long-running operations.

    ```c++
    void lisp_set_cycle_yield(yield_def yield);
    ```

    Define a yield function that conforms to the `yield_def` type:

    ```c++
    typedef void (*yield_def)();

    void my_yield_function() {
        // Perform yield operations, such as yielding control to an event loop
    }
    ```

    Register the yield function:

    ```c++
    lisp_set_cycle_yield(my_yield_function);
    ```
*   **`lisp_set_printers`**: Configures output handlers for standard output, logs, and errors.

    ```c++
    void lisp_set_printers(print_def out, print_def log, print_def err);
    ```

### System Information

*   **`lisp_mem_used`**: Retrieves the amount of memory used.

    ```c++
    size_t lisp_mem_used(void);
    ```
*   **`lisp_error_idx`**: Gets the current index in the input buffer where an error occurred.

    ```c++
    int lisp_error_idx(void);
    ```

## Conclusion

**UniotLisp** offers a lightweight yet powerful Lisp interpreter suitable for embedding within C applications. Its minimalist design ensures ease of integration, while its extensible architecture allows developers to tailor its capabilities to specific requirements. By understanding its core concepts, utilizing built-in primitives, and leveraging the ability to add custom functionalities, developers can effectively harness UniotLisp for a variety of applications.

For further assistance or to contribute to the project, please refer to the project's repository or contact the maintainers.
