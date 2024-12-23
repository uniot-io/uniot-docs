# ConfigCaptivePortal

The `ConfigCaptivePortal` class provides a captive portal web server that allows users to configure network settings through a web interface. It handles DNS requests to redirect clients to the configuration page and serves the necessary HTML content for setting up WiFi credentials. This facilitates an easy and user-friendly method for configuring the device's network parameters without requiring direct access to the device's firmware.

**Constructor:**

* **`ConfigCaptivePortal(const IPAddress &apIp)`**\
  Initializes the DNS server and web server instances with the provided access point IP. Sets the initial state to not started and prepares the captive portal for handling client requests.

**Methods:**

* **`bool start()`**\
  Starts the captive portal by initializing the DNS and web servers.

* **`void stop()`**\
  Stops the captive portal by terminating the DNS and web servers.

* **`void reset()`**\
  Resets the captive portal by reinitializing the DNS and web server instances.

* **`WebServer* get()`**\
  Retrieves the web server instance managed by the captive portal.

* **`const IPAddress& ip() const`**\
  Retrieves the IP address assigned to the access point.

* **`void execute(short _) override`**\
  Processes DNS requests and handles web server clients.

**Private Members:**

* **`bool mIsStarted`**\
  Indicates whether the captive portal is currently active.

* **`IPAddress mApIp`**\
  IP address assigned to the access point for the captive portal.

* **`UniquePointer<DNSServer> mpDnsServer`**\
  Unique pointer to the DNS server instance handling DNS requests for the captive portal.

* **`UniquePointer<WebServer> mpWebServer`**\
  Unique pointer to the web server instance serving the captive portal pages.

### Type Definitions

* **`#define DNS_PORT 53`**\
  Defines the DNS port number used by the DNS server.

* **`#define HTTP_PORT 80`**\
  Defines the HTTP port number used by the web server.

* **`#define DOMAIN_NAME "*"`**\
  Defines the domain name pattern to match all DNS queries, redirecting them to the captive portal.
