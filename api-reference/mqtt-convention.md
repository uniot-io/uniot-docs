# MQTT Convention

The Uniot Platform uses the Message Queuing Telemetry Transport (MQTT) protocol to manage and communicate with IoT devices. MQTT is a lightweight, publish-subscribe network protocol that transports messages between devices. In the context of Uniot, it is important to understand the conventions followed, such as the MQTT topic structure, payload types, Quality of Service (QoS) levels, and other specifics. This section will provide you with an in-depth understanding of these concepts.

## MQTT Protocol Version

Uniot relies on MQTT protocol version 3.1.1, as it is the most widespread and well-supported version across various devices and platforms. This choice ensures that the Uniot platform maintains compatibility and efficiency, aligning with industry standards and facilitating seamless integration with a broad range of IoT devices and systems.

## MQTT Topic Structure

In the Uniot Platform, MQTT topics are structured to ensure logical organization and efficient communication.

## Payload Types

While the primary payload type used by the Uniot Platform is CBOR (Concise Binary Object Representation), the platform's flexible architecture allows users to create custom topics tailored to their specific needs and third-party applications. In such cases, any data format can be employed, providing the freedom to choose the most suitable format for specific use cases. This flexibility ensures that Uniot can be seamlessly integrated with a wide range of devices and systems without sacrificing efficiency or compatibility.

## Quality of Service (QoS) Levels

The Uniot Platform supports different QoS levels to ensure message delivery according to the requirements:

* **QoS 0:** At most once delivery. The message is sent, but there's no acknowledgment required.
* **QoS 1:** At least once delivery. The message is guaranteed to arrive but may be duplicated.
* _**QoS 2:** There is no application. Therefore it is not supported by own MQTT broker and clients._

## Retained Messages

In Uniot's MQTT convention, messages can be retained to ensure that the latest value of a topic is stored on the broker and is immediately available to new subscribers. This is particularly useful for status topics, where the latest state is always relevant.

## Last Will and Testament (LWT)

Devices provide a "last will" message that the Broker will send on their behalf if they disconnect unexpectedly. This is used to alert other devices or systems to a potential problem.

## Uniot Core and Automation

Uniot Core is designed to easily adhere to the described MQTT convention. It provides a user-friendly interface that facilitates the addition of new types of sensors and actuators. These additions are accompanied by automatic descriptions of the required topics and message types. Such automation simplifies the configuration process and ensures consistency across different devices and applications within the Uniot ecosystem.

## Conclusion

The Uniot Platform's MQTT convention, coupled with Uniot Core's adaptability and support for multiple data types, provides a robust foundation for building and managing IoT solutions. Developers, integrators and end users can leverage this convention and flexibility to create applications that meet their unique requirements and standards.



