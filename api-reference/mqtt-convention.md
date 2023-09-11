# MQTT Convention

The Uniot Platform uses the Message Queuing Telemetry Transport (MQTT) protocol to manage and communicate with IoT devices. MQTT is a lightweight, publish-subscribe network protocol that transports messages between devices. In the context of Uniot, it is important to understand the conventions followed, such as the MQTT topic structure, payload types, Quality of Service (QoS) levels, and other specifics. This section will provide you with an in-depth understanding of these concepts.

## MQTT Protocol Version

Uniot relies on MQTT protocol version 3.1.1, as it is the most widespread and well-supported version across various devices and platforms. This choice ensures that the Uniot platform maintains compatibility and efficiency, aligning with industry standards and facilitating seamless integration with a broad range of IoT devices and systems.

## MQTT Topic Structure

In the Uniot Platform, MQTT topics are structured to ensure logical organization and efficient communication.

### **Device Communication**

1. **Device Online Status & Capabilities**
   * **Topic Format:** `<domain>/users/<userId>/devices/<deviceId>/status`
   * **Purpose:** Denotes the online/offline status and provides key device metadata.
   *   **Message Example (CBOR rendered as JSON):**

       ```json
       {
         "online": 1,
         "id": 0,
         "primitives": ["device_write", "device_read", "analog_write", "analog_read", "button_clicked"],
         "creator": "UNIOT",
         "mqtt_size": 1024,
         "d_in": 3,
         "d_out": 3,
         "a_in": 1,
         "a_out": 3,
         "timestamp": 1679968923
       }

       ```
2. **Device Command and Scripting**
   * **Topic Format:** `<domain>/users/<userId>/devices/<deviceId>/script`
   * **Purpose:** For sending command scripts to devices.
   *   **Message Example (CBOR rendered as JSON):**

       ```json
       {
         "runtime": "uLisp",
         "version": "0.1.3",
         "code": "(task 30 300 ' (list (device_write 0 (= (% #t_pass 2) 0))))",
         "timestamp": 1679968928
       }

       ```

### **Event Communication**

1. **User Device Events**
   * **Topic Format:** `<domain>/users/<userId>/devices/<deviceId>/event/<eventID>`
   * Users can create custom event types and publish messages to them.
   *   **Message Example (CBOR rendered as JSON):**

       ```json
       {
         "eventID": "rgb",
         "value": 5007612,
         "sender": {
           "type": "device",
           "id": "c8c9a30bdf9c"
         },
         "timestamp": 1679968935
       }
       ```
2. **User Group Events**
   * **Topic Format:** `<domain>/users/<userId>/groups/<groupId>/event/<eventID>`
3. **Shared Group Events (Open to multiple users)**
   * **Topic Format:** `<domain>/groups/shared/<sharedGroupId>/event/<eventID>`

### **Group Classification**

1.  **Personal Groups:** These are user-specific groups, where devices belonging to a single user are grouped together based on some criteria (e.g., function, location, or device type).

    Topic: `<domain>/users/<userId>/groups/<groupId>/event/<eventID>`

    Or: `<domain>/groups/private/<privateGroupId>/event/<eventID>`
2.  **Shared Groups:** These are groups where devices from different users can join and share data or events.

    Topic: `<domain>/groups/shared/<sharedGroupId>/event/<eventID>`
3.  **Public Groups:** These might be open groups where any device or user can join, and data is made public for anyone to subscribe to. This could be useful for open-source projects or community-driven initiatives.

    Topic: `<domain>/groups/public/<publicGroupId>/event/<eventID>`
4.  **Collaborative Groups:** This is a blend of personal and shared groups. Here, a user can create a group and invite specific users to join. Only invited users can contribute, but all members can view or act on the data.

    Topic: `<domain>/groups/collab/<collabGroupId>/event/<eventID>`
5.  **Role-based Groups:** Devices are grouped based on roles. For instance, in a smart home setup, you might have groups like 'Security Devices', 'Entertainment Devices', etc.

    Topic: `<domain>/groups/role/<roleGroupId>/event/<eventID>`
6.  **Geo-based Groups:** Devices are grouped based on their geographical locations, useful for scenarios like smart city implementations where devices in a particular area or region might need to communicate more frequently.

    Topic: `<domain>/groups/geo/<geoGroupId>/event/<eventID>`

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



