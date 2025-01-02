# DefaultPrimitives

The `DefaultPrimitives` component defines a set of primitives essential for interacting with hardware. These primitives serve as the bridge between Lisp scripts and the underlying system functionalities, enabling seamless communication and control.

**Member Variables:**

- **`constexpr const char* dwrite`**
  Represents the [`dwrite`](../appkit/lispprimitives.md) primitive, responsible for writing the analog data to a specified GPIO pin.

- **`constexpr const char* dread`**
  Represents the [`dread`](../appkit/lispprimitives.md) primitive, responsible for reading the current analog data from a specified GPIO pin.

- **`constexpr const char* awrite`**
  Represents the [`awrite`](../appkit/lispprimitives.md) primitive, responsible for writing the analog data to a specified GPIO pin.

- **`constexpr const char* aread`**
  Represents the [`aread`](../appkit/lispprimitives.md) primitive, responsible for reading the current analog data from a specified GPIO pin.

- **`constexpr const char* bclicked`**
  Represents the [`bclicked`](../appkit/lispprimitives.md) primitive, responsible for handling button click.
