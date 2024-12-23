# Network

The `Network` module is a critical component of the Uniot project, responsible for managing all aspects of network connectivity and configuration. It ensures reliable WiFi connections, facilitates user interactions for network setup, and provides a seamless interface for configuring network parameters through a captive portal. The module is designed to work across different ESP platforms (ESP8266 and ESP32), leveraging platform-specific capabilities to deliver robust network management.

### Components

[**NetworkController**](networkcontroller.md)

The `NetworkController` class manages network configurations, user interactions through buttons, and status indicators using LEDs. It integrates with the `NetworkScheduler` to handle connection events, manage reboot logic based on connection stability, and ensure that the device maintains a reliable network connection. The controller also handles user-initiated actions such as reconnecting to the network or resetting network configurations.

[**NetworkScheduler**](networkscheduler.md)

The `NetworkScheduler` class oversees network-related tasks, including initiating WiFi connections, managing a captive portal for network setup, and monitoring the network status. It interacts with the `TaskScheduler` to schedule and execute tasks that handle various network states, ensuring that the device can connect to available networks, fallback to an access point mode when necessary, and recover from connection failures gracefully.

[**ConfigCaptivePortal**](configcaptiveportal.md)

The `ConfigCaptivePortal` class provides a captive portal web server that allows users to configure network settings through a web interface. It handles DNS requests to redirect clients to the configuration page and serves the necessary HTML content for setting up WiFi credentials. This facilitates an easy and user-friendly method for configuring the device's network parameters without requiring direct access to the device's firmware.

### Overview

Together, these components form a cohesive system that manages network connectivity, user interactions, and configuration processes. The **Network** module ensures that the Uniot device can seamlessly connect to WiFi networks, provide a user-friendly setup interface, and maintain stable network operations across different environments and use cases.

