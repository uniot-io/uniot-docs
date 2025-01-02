# EventListener

The `EventListener` class extends [`EventEmitter`](eventemitter.md) and allows components to subscribe to specific events. It maintains a list of topics it is interested in and defines a pure virtual method `onEventReceived` that must be implemented to handle incoming events.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`EventListener *listenToEvent(T_topic topic)`**\
  Subscribes the listener to a specific event topic, enabling it to receive events associated with that topic.

* **`EventListener *stopListeningToEvent(T_topic topic)`**\
  Unsubscribes the listener from a specific event topic, preventing it from receiving events associated with that topic.

* **`bool isListeningToEvent(T_topic topic)`**\
  Checks whether the listener is currently subscribed to a specific event topic.

* **`virtual void onEventReceived(T_topic topic, T_msg msg) = 0`**\
  Pure virtual method that must be implemented by derived classes to define how events are handled when received.

**Private Members:**

* **`ClearQueue<T_topic> mTopics`**\
  A queue maintaining a list of event topics the listener is subscribed to.
