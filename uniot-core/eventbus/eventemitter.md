# EventEmitter

The `EventEmitter` class extends [`EventEntity`](evententity.md) and provides functionalities to emit events to the [`EventBus`](eventbus.md). It acts as a bridge between components that generate events and the EventBus that dispatches them to listeners, enabling seamless event-driven interactions within the system.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`void emitEvent(T_topic topic, T_msg msg)`**\
  Emits an event with the specified topic and message to the EventBus, triggering the execution of event handlers in subscribed listeners.
