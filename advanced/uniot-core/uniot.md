# Uniot

The `Uniot` component is responsible for managing core functionalities such as event handling and task scheduling within the Uniot Core. It initializes essential services, sets up task schedulers for handling events and date storage, and provides interfaces for interacting with the event bus and scheduler.

**Constructor:**

* **`UniotCore()`**\
  Constructs a `UniotCore` instance and initializes the task scheduler and event bus with a unique identifier.

**Methods:**

* **`void begin(uint32_t eventBusTaskPeriod = 10, uint32_t storeDateTaskPeriod = 5 * 60 * 1000UL)`**\
  Initializes the core services by setting up task schedulers for event handling and date storage. Configures logging to indicate readiness and attaches tasks with specified periods to the scheduler.

* **`void loop()`**\
  Executes the main loop by invoking the scheduler's loop method, allowing scheduled tasks to run and events to be processed.

* **`uniot::CoreEventBus& getEventBus()`**\
  Retrieves a reference to the [`CoreEventBus`](eventbus/eventbus.md) instance, enabling interaction with the event bus for event-driven operations.

* **`uniot::TaskScheduler& getScheduler()`**\
  Retrieves a reference to the [`TaskScheduler`](scheduler/taskscheduler.md) instance, allowing for the management and scheduling of system tasks.

**Private Members:**

* **`uniot::TaskScheduler mScheduler`**\
  Manages the scheduling and execution of tasks within the Uniot system, ensuring that tasks run at their designated intervals.

* **`uniot::CoreEventBus mEventBus`**\
  Handles the registration, broadcasting, and handling of events within the Uniot system, facilitating communication between different system components.
