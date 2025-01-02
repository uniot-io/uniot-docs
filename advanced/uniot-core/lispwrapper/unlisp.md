# unLisp

The `unLisp` class is responsible for managing the Lisp execution environment, handling primitive registrations, and facilitating the evaluation of Lisp scripts. As a singleton, it ensures that only one instance of the Lisp environment exists throughout the application's lifecycle, providing a unified interface for Lisp interactions.

**Methods:**

* **`TaskScheduler::TaskPtr getTask()`**\
  Retrieves the task pointer responsible for managing Lisp evaluation cycles.

* **`bool isCreated()`**\
  Checks whether the Lisp execution environment has been created.

* **`bool taskIsRunning()`**\
  Determines whether the Lisp evaluation task is currently attached and running.

* **`size_t memoryUsed()`**\
  Retrieves the amount of memory currently used by the Lisp environment.

* **`void runCode(const Bytes &data)`**\
  Executes the provided Lisp code within the Lisp environment.

* **`unLisp *pushPrimitive(Primitive *primitive)`**\
  Adds a new primitive to the Lisp environment, facilitating its invocation within Lisp scripts.

* **`void serializePrimitives(CBORObject &obj)`**\
  Serializes the currently registered primitives into a CBOR object for persistent storage or transmission.

* **`const Bytes &getLastCode()`**\
  Retrieves the most recently executed Lisp code.

* **`void cleanLastCode()`**\
  Clears the record of the last executed Lisp code.

* **`virtual void onEventReceived(unsigned int topic, int msg) override`**\
  Handles events received by the `unLisp` instance, allowing Lisp scripts to respond to system events.

**Private Members:**

* **`Bytes mLastCode`**\
  Stores the most recently executed Lisp code.

* **`TaskScheduler::TaskPtr mTaskLispEval`**\
  Pointer to the task responsible for Lisp code evaluation.

* **`ClearQueue<Pair<String, Primitive *>> mUserPrimitives`**\
  Queue holding user-defined primitives, each paired with its name.

* **`const Primitive *mPrimitiveTask`**\
  Pointer to the primitive handling task operations.

* **`const Primitive *mPrimitiveIsEventAvailable`**\
  Pointer to the primitive checking event availability.

* **`const Primitive *mPrimitivePopEvent`**\
  Pointer to the primitive for popping events.

* **`const Primitive *mPrimitivePushEvent`**\
  Pointer to the primitive for pushing events.

* **`void *mLispEnvConstructor[3]`**\
  Array used for constructing the Lisp environment.

* **`Root mLispRoot`**\
  Pointer to the Lisp root environment.

* **`VarObject mLispEnv`**\
  Pointer to the Lisp environment variables.

* **`Map<String, SharedPointer<LimitedQueue<Bytes>>> mIncomingEvents`**\
  Map managing incoming events, each associated with a unique event ID and a limited queue of event data.
