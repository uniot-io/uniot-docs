# DataChannels

The `DataChannels` class manages data transmission associated with different event topics within the EventBus system. It ensures that data sent to specific channels is stored and retrieved efficiently, maintaining data integrity and access control.

**Template Parameters:**

* **`T_channel`**\
  The type representing the data channel identifier.

* **`T_data`**\
  The type of data to be transmitted through the channels.

**Methods:**

* **`bool open(T_channel channel, size_t limit)`**\
  Opens a new data channel for the specified topic with a defined limit on the number of data items it can hold.

* **`bool close(T_channel channel)`**\
  Closes an existing data channel, removing it from management.

* **`bool send(T_channel channel, T_data data)`**\
  Sends data to the specified channel. If the channel is full, it overwrites the oldest data to accommodate the new entry.

* **`T_data receive(T_channel channel)`**\
  Retrieves and removes the oldest data item from the specified channel.

* **`bool isEmpty(T_channel channel)`**\
  Checks whether the specified data channel is empty.

**Private Members:**

* **`Map<T_channel, SharedPointer<LimitedQueue<T_data>>> mChannels`**\
  A map associating each data channel with its corresponding limited queue for data storage.
