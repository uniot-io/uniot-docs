# LispHelper

The `LispHelper` component provides a suite of utility functions and definitions that facilitate the integration and management of Lisp. Serving as a foundational layer, it simplifies the interaction between Lisp scripts and the underlying system by offering type definitions, type-checking mechanisms, and helper functions.

**Methods:**

* **`static inline bool correct(Lisp::Type type)`**\
  Validates whether the provided type falls within the defined range of Lisp types.

* **`static inline const char *str(Lisp::Type type)`**\
  Retrieves the string representation of the specified Lisp type.

* **`static inline Lisp::Type getType(lisp::Object obj)`**\
  Determines the Lisp type of the provided Lisp object.
