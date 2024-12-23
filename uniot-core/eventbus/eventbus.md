# EventBus

The `EventBus` class is the core of the EventBus module, responsible for managing event entities, dispatching events, and maintaining data channels. It handles the registration and unregistration of event listeners and ensures that events are delivered to the appropriate subscribers in an orderly and efficient manner.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`void registerKit(IEventBusConnectionKit<T_topic, T_msg, T_data> &connection)`**\
  Registers a connection kit with the EventBus, allowing it to establish or manage connections with event entities.

* **`void unregisterKit(IEventBusConnectionKit<T_topic, T_msg, T_data> &connection)`**\
  Unregisters a connection kit from the EventBus, severing its connections with event entities.

* **`bool registerEntity(EventEntity<T_topic, T_msg, T_data> *entity)`**\
  Registers an event entity (listener or emitter) with the EventBus, enabling it to participate in event dispatching.

* **`void unregisterEntity(EventEntity<T_topic, T_msg, T_data> *entity)`**\
  Unregisters an event entity from the EventBus, removing it from event dispatching.

* **`bool openDataChannel(T_topic topic, size_t limit)`**\
  Opens a data channel for a specific event topic with a defined data limit.

* **`bool closeDataChannel(T_topic topic)`**\
  Closes a data channel associated with a specific event topic.

* **`bool sendDataToChannel(T_topic topic, T_data data)`**\
  Sends data to the specified data channel associated with an event topic.

* **`T_data receiveDataFromChannel(T_topic topic)`**\
  Receives data from the specified data channel associated with an event topic.

* **`bool isDataChannelEmpty(T_topic topic)`**\
  Checks whether the specified data channel is empty.

* **`void emitEvent(T_topic topic, T_msg msg)`**\
  Emits an event with the specified topic and message, dispatching it to all registered listeners.

* **`virtual void execute(short _) override`**\
  Processes queued events, ensuring they are dispatched to the appropriate listeners in an orderly manner.

**Private Members:**

* **`ClearQueue<EventEntity<T_topic, T_msg, T_data> *> mEntities`**\
  A queue maintaining pointers to all registered event entities.

* **`ClearQueue<Pair<T_topic, T_msg>> mEvents`**\
  A queue storing events that need to be dispatched to listeners.

* **`DataChannels<T_topic, T_data> mDataChannels`**\
  Manages data channels associated with different event topics.

* **`unsigned int mId`**\
  A unique identifier for the EventBus instance.
