# Storage

The `Storage` module is a fundamental component of the Uniot Core, responsible for managing persistent data storage. It abstracts the complexities of different file systems, providing a unified interface for storing, retrieving, and managing data. The module ensures reliable data persistence across device restarts and facilitates structured data handling through CBOR serialization. Additionally, it offers specialized functionality for logging crash information, aiding in debugging and system reliability.

### Components

[**Storage**](storage.md)

The `Storage` class serves as the core component for handling file system operations. It abstracts the underlying file system differences between ESP8266 and ESP32 platforms by utilizing `SPIFFS` or `LittleFS` based on configuration. This class provides methods to store, restore, and clean data from specified file paths, ensuring efficient and reliable data management. It also manages the mounting and unmounting of the file system, optimizing resource usage by tracking active instances.

[**CBORStorage**](cborstorage)

The `CBORStorage` class extends the `Storage` class to support structured data management using CBOR (Concise Binary Object Representation). This allows for efficient serialization and deserialization of complex data structures, making it ideal for storing configuration settings and other structured information. By leveraging CBOR, `CBORStorage` ensures that data is stored in a compact and easily parsable format, enhancing the versatility and scalability of the storage solutions within the Uniot framework.

[**CrashStorage**](crashstorage.md)

The `CrashStorage` class is a specialized extension of the `Storage` class designed exclusively for the ESP8266 platform. It captures and logs crash information, including reset reasons and stack traces, to aid in post-mortem analysis and debugging. By storing detailed crash dumps, `CrashStorage` provides valuable insights into system failures, enabling developers to diagnose and rectify issues effectively. This class ensures that critical crash data is preserved across device restarts, contributing to the overall robustness and reliability of the Uniot system.

[**WifiStorage**](wifistorage.md)

The `WifiStorage` class extends the `CBORStorage` class to manage WiFi credentials securely and efficiently. It handles the storage, retrieval, and validation of WiFi SSIDs and passwords, facilitating seamless network connections. By leveraging CBOR for data serialization, `WifiStorage` ensures that WiFi credentials are stored in a structured and compact format. This class provides methods to set, get, and verify the validity of stored credentials, enabling reliable network configuration and reconnection processes within the Uniot framework.
