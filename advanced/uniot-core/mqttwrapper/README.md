# MQTTWrapper

The `MQTTWrapper` module is designed to facilitate seamless integration with MQTT protocols. This module provides a robust and flexible framework for managing MQTT devices, handling message publishing and subscribing. By encapsulating the complexities of MQTT interactions, this module enables to focus on building responsive and scalable applications without worrying about the underlying communication intricacies.

### Components

[**MQTTDevice**](mqttdevice.md)

Provides essential functionalities for subscribing to MQTT topics, publishing messages, and handling incoming messages. By encapsulating the core MQTT operations, `MQTTDevice` simplifies the integration of MQTT communication.

[**CallbackMQTTDevice**](callbackmqttdevice.md)

Extends the `MQTTDevice` class by incorporating callback functionalities, enabling customized handling of incoming MQTT messages. This class allows to define specific behaviors in response to received messages, facilitating dynamic and responsive device interactions.

[**MQTTPath**](mqttpath.md)

Manages the construction of MQTT topic paths based on device and owner credentials. The `MQTTPath` class provides methods to build device-specific, group-specific, and public topic paths, ensuring organized and secure topic management within the MQTT broker.

[**MQTTKit**](mqttkit.md)

Manages connections to the MQTT broker, oversees multiple `MQTTDevice` instances, handles message publishing and subscribing, and ensures secure and efficient communication through COSE message handling. By integrating with network and time synchronization events, `MQTTKit` provides a robust and reliable foundation for MQTT-based interactions.
