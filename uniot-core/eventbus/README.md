# EventBus

The `EventBus` module is a fundamental component within the Uniot Core, designed to facilitate efficient and organized event-driven communication between different parts of the system. Leveraging the principles of the Observer pattern, the EventBus enables decoupled interaction between publishers and subscribers, promoting modularity and scalability.

### Components

[**EventBus**](eventbus.md)

The `EventBus` class is the core of the EventBus module, responsible for managing event entities, dispatching events, and maintaining data channels. It handles the registration and unregistration of event listeners and ensures that events are delivered to the appropriate subscribers in an orderly and efficient manner.

[**IEventBusConnectionKit**](ieventbusconnectionkit.md)

The `IEventBusConnectionKit` interface defines the contract for classes that wish to establish connections with the `EventBus`. Implementing this interface allows classes to register and unregister themselves appropriately, managing their participation in event-driven communication.

[**DataChannels**](datachannels.md)

The `DataChannels` class manages data transmission associated with different event topics within the EventBus system. It ensures that data sent to specific channels is stored and retrieved efficiently, maintaining data integrity and access control.

[**EventEmitter**](eventemitter.md)

The `EventEmitter` class extends `EventEntity` and provides functionalities to emit events to the `EventBus`. It acts as a bridge between components that generate events and the EventBus that dispatches them to listeners.

[**EventListener**](eventlistener.md)

The `EventListener` class extends `EventEmitter` and allows components to subscribe to specific events. It maintains a list of topics it is interested in and defines a pure virtual method `onEventReceived` that must be implemented to handle incoming events.

[**EventEntity**](evententity.md)

The `EventEntity` class serves as a base for both emitters and listeners within the EventBus system. It maintains a queue of connected EventBus instances and provides mechanisms to interact with them, such as sending and receiving data through channels.

[**CallbackEventListener**](callbackeventlistener.md)

The `CallbackEventListener` class provides a mechanism for handling events by allowing the registration of callback functions. This enables to define custom behaviors that should occur when specific events are emitted, without the need to create specialized listener classes.
