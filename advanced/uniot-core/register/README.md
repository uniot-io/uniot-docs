# Register

The `Register` module is designed to manage and facilitate the registration and handling of various system entities. This module provides a flexible and extensible framework for registering GPIO pins, objects, and managing their associations.

### Components

[**GpioRegister**](gpioregister.md)

Specializes the generalized `Register` class to handle GPIO (General Purpose Input/Output) pin management. It provides dedicated methods for configuring GPIO pins as digital or analog inputs and outputs, ensuring seamless integration with the underlying hardware.

[**ObjectRegister**](objectregister.md)

Extends the `Register` class to manage the registration and retrieval of complex system objects. It facilitates linking named objects with unique identifiers and ensures that only valid and active records are accessible, enhancing the robustness and reliability of object management.

[**ObjectRegisterRecord**](objectregisterrecord.md)

Serves as a foundational component for managing object records within the Register module. It tracks the active status of registered objects, ensuring that only valid and existing records are accessible, thereby enhancing the integrity and reliability of object management.

[**Register**](register.md)

A versatile and generalized template class that provides a flexible framework for creating specialized register classes. It facilitates the storage, retrieval, and management of system entities in a type-safe and efficient manner, serving as the backbone for both GPIO and object registrations.

[**RegisterManager**](registermanager.md)

Acts as the central orchestrator within the Register module, overseeing the registration and management of both GPIO pins and complex system objects. It provides a unified interface for configuring hardware resources and linking objects, ensuring organized and efficient resource management across the Uniot system.

[**RegisterManagerProxy**](registermanagerproxy.md)

Functions as an intermediary between client classes and the central `RegisterManager`, facilitating controlled and streamlined interactions with registered entities. By abstracting direct access to the `RegisterManager`, it promotes decoupled and modular design, enhancing the flexibility and maintainability of the Uniot system.
