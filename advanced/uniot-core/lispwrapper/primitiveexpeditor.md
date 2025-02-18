# PrimitiveExpeditor

The `PrimitiveExpeditor` class is responsible for defining, describing, and managing Lisp primitives. Serving as an intermediary between Lisp scripts and system functionalities, it facilitates the registration and invocation of primitives, ensuring that Lisp code can effectively interact with the underlying Uniot system.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`static RegisterManager &getRegisterManager()`**\
  Retrieves the singleton instance of the [`RegisterManager`](../register/registermanager.md) responsible for managing primitive registers.

* **`static PrimitiveExpeditorInitializer describe(const String &name, Lisp::Type returnType, int argsCount, ...)`**\
  Describes a primitive by specifying its name, return type, number of arguments, and expected argument types. This method facilitates the definition of primitive characteristics before registration.
  * **`name`** (`const String &`): The name of the primitive.
  * **`returnType`** (`Lisp::Type`): The expected return type of the primitive.
  * **`argsCount`** (`int`): The number of arguments the primitive accepts.
  * **`...`** (`Lisp::Type`): A variable number of arguments specifying the expected types of each argument.

* **`static PrimitiveDescription extractDescription(Primitive *primitive)`**\
  Extracts the description of a given primitive, capturing its name, argument count, argument types, and return type.

* **`RegisterManagerProxy &getAssignedRegister()`**\
  Retrieves the proxy to the `RegisterManager`, allowing for managed interactions with primitive registers.

* **`int getArgsLength()`**\
  Retrieves the number of arguments provided to a primitive invocation.

* **`bool checkType(Object param, Lisp::Type expectedType)`**\
  Checks whether a given Lisp object matches the expected type.

* **`Object evalList()`**\
  Evaluates the current Lisp list within the environment and root context, returning the evaluated object.

* **`Object list()`**\
  Retrieves the current Lisp list without evaluation.

* **`Object evalObj(VarObject obj)`**\
  Evaluates a specific Lisp object within the environment and root context.

* **`void terminate(const char *msg)`**\
  Terminates the primitive execution with an error message.

* **`void assertArgsCount(int length)`**\
  Asserts that the number of provided arguments matches the expected count, triggering an error if not.

* **`void assertArgs(uint8_t length, const Lisp::Type *types)`**\
  Asserts that the provided arguments match the expected types and counts, triggering an error if discrepancies are found.

* **`void assertArgs(uint8_t length, ...)`**\
  Overloaded method to assert argument types using a variable number of type parameters.

* **`void assertDescribedArgs()`**\
  Asserts that the provided arguments match the description defined during primitive description.

* **`Object getArg(int idx)`**\
  Retrieves the argument at the specified index from the current Lisp invocation context.

* **`bool getArgBool(int idx, bool acceptsInt = true)`**\
  Retrieves a boolean argument from the specified index, optionally accepting integers as boolean representations.

* **`int getArgInt(int idx, bool acceptsBool = true)`**\
  Retrieves an integer argument from the specified index, optionally accepting booleans as integer representations.

* **`const char *getArgSymbol(int idx)`**\
  Retrieves a symbol argument from the specified index.

* **`Object makeBool(bool value)`**\
  Creates a Lisp boolean object based on the provided value.

* **`Object makeInt(int value)`**\
  Creates a Lisp integer object based on the provided value.

* **`Object makeSymbol(const char *value)`**\
  Creates a Lisp symbol object based on the provided string.

**Private Members:**

* **`PrimitiveDescription mDescription`**\
  Stores the description of the current primitive, including its name, argument count, argument types, and return type.

* **`Root mRoot`**\
  Pointer to the Lisp root environment.

* **`VarObject mEnv`**\
  Pointer to the Lisp environment variables.

* **`VarObject mList`**\
  Pointer to the current Lisp list being processed.

* **`Object mEvalList`**\
  Stores the result of evaluating the current Lisp list.

* **`RegisterManagerProxy mRegisterProxy`**\
  Proxy instance for managing primitive registrations with the `RegisterManager`.

* **`static RegisterManager sRegister`**\
  Singleton instance of the `RegisterManager` responsible for managing all primitive registrations.

* **`static jmp_buf sDescriptionJumper`**\
  Jump buffer used for handling primitive description interruptions.

* **`static PrimitiveDescription sLastDescription`**\
  Stores the most recently described primitive's description.

* **`static bool DescriptionModeGuard::sDescriptionMode`**\
  Static flag indicating whether the system is in description mode.
