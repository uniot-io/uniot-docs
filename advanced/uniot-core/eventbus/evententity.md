# EventEntity

The `EventEntity` class serves as a base for all entities that interact with the [`EventBus`](eventbus.md), including both listeners and emitters. It manages the connection to the EventBus and provides foundational functionalities for event-driven communication.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`bool sendDataToChannel(T_topic channel, T_data data)`**\
  Sends data to a specific data channel associated with an event topic across all connected EventBus instances.

* **`void receiveDataFromChannel(T_topic channel, DataChannelCallback callback)`**\
  Receives data from a specific data channel associated with an event topic and executes a callback function with the received data.

* **`virtual type_id getTypeId() const override`**\
  Retrieves the unique type identifier for the `EventEntity` class, facilitating safe type casting.

**Private Members:**

* **`IterableQueue<EventBus<T_topic, T_msg, T_data> *> mEventBusQueue`**\
  A queue maintaining pointers to connected EventBus instances.
