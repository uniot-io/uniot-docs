# CallbackEventListener

The `CallbackEventListener` class provides a mechanism for handling events by allowing the registration of callback functions. This enables to define custom behaviors that should occur when specific events are emitted, without the need to create specialized listener classes.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* `CallbackEventListener(EventListenerCallback callback)`\
  Constructs a `CallbackEventListener` with the specified callback function.

* `void onEventReceived(T_topic topic, T_msg msg)`\
  Invoked when an event matching the subscribed topic is received. Executes the registered callback function with the event's topic and message.

  * **`topic`** (`T_topic`): The topic of the received event.
  * **`msg`** (`T_msg`): The message associated with the received event.

**Private Members:**

* **`EventListenerCallback mCallback`**\
  Stores the callback function to be executed upon receiving an event.
