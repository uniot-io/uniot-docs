# Singleton

The `Singleton` utility implements the Singleton design pattern, ensuring that a class has only one instance throughout the application's lifecycle and providing a global point of access to that instance. This pattern is particularly beneficial in scenarios where a single shared resource or manager is required.

**Key Features:**

- Prevents multiple instances of a class.
- Provides controlled access to the single instance.
- Utilizes modern C++ features like templates and static local variables for efficient implementation.
- Thread-safe initialization since C++11.

**Template Parameters:**

* **`Derived`**\
The class that inherits from Singleton. This allows the Singleton utility to manage the instantiation and access of the `Derived` class.

**Constructors and Destructor:**

* **`Singleton()`**\
Protected default constructor ensures that only derived classes can instantiate the Singleton.

* **`~Singleton()`**\
Protected destructor ensures controlled destruction of the Singleton instance.

**Assignment Operators:**

* **`Singleton(const Singleton&) = delete;`**\
Deletes the copy constructor to prevent copying of the Singleton instance.

* **`Singleton& operator=(const Singleton&) = delete;`**\
Deletes the copy assignment operator to prevent assignment of the Singleton instance.

**Methods:**

* **`static inline Derived& getInstance()`**\
Provides access to the single instance of the Derived class. If the instance does not exist, it is created upon the first call.
