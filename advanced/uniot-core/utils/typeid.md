# TypeId

The `TypeId` utility provides a lightweight and efficient mechanism for runtime type identification and safe type casting without relying on traditional C++ Run-Time Type Information (RTTI).

**Key Features:**

- **Lightweight Type Identification:** Uses unique pointers as type identifiers.
- **Interface for Type Retrieval:** Provides a standardized way to retrieve an object's type identifier.
- **Safe Static Casting:** Enables safe casting between base and derived classes based on type identifiers.
- **Template-Based Design:** Leverages C++ templates for type-safe operations.

**Methods:**

* **`template <class T> static inline type_id getTypeId()`**\
Generates a unique type identifier for the specified type `T`. This is achieved by using the address of a static pointer unique to each type.

* **`template <typename T> static inline T* safeStaticCast(IWithType* obj)`**\
Safely casts an object of type `IWithType*` to `T*` if the object's type identifier matches that of type `T`. If the types do not match, the method logs a debug message and returns `nullptr`.
