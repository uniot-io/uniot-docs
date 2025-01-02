# IEventBusConnectionKit

The `IEventBusConnectionKit` interface defines the contract for classes that wish to establish connections with the [`EventBus`](eventbus.md). Implementing this interface allows classes to register and unregister themselves appropriately, managing their participation in event-driven communication.

**Template Parameters:**

* **`T_topic`**\
  The type representing the event topic identifier.

* **`T_msg`**\
  The type representing the event message.

* **`T_data`**\
  The type representing the data associated with the event.

**Methods:**

* **`virtual void registerWithBus(EventBus<T_topic, T_msg, T_data> &eventBus) = 0`**\
  Registers the connection kit with the specified EventBus instance, establishing the necessary connections for event communication.

* **`virtual void unregisterFromBus(EventBus<T_topic, T_msg, T_data> &eventBus) = 0`**\
  Unregisters the connection kit from the specified EventBus instance, severing all established connections.
