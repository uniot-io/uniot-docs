# Edge Logic Deployment

## **Why** Uniot uses Edge Logic Deployment instead of imperative or declarative models

At Uniot, we have chosen **Edge Logic Deployment** as the foundation of our system. This approach allows for the **dynamic deployment of executable logic** to edge devices, where it is processed by the **Edge Logic Engine**, a runtime responsible for **interpreting and executing automation scripts locally**. Unlike traditional IoT models that rely on centralized cloud control, this system enables **autonomous decision-making at the device level**. The **Edge Logic Engine** runs deployed logic using [UniotLisp](../advanced/uniot-lisp/), a lightweight scripting language optimized for real-time execution in resource-constrained environments. Together, these components ensure that devices can **react to events, execute scripts efficiently, and adapt to changing conditions - without requiring constant network connectivity or firmware updates**.

Traditional IoT systems rely on **imperative** or **declarative** control models, but both have limitations that make them inefficient for scalable, adaptive automation. Below, we compare these models and explain why **Edge Logic Deployment** is more powerful.

***

## **Traditional IoT control models and their limitations**

### **Imperative model: direct commands**

In the **imperative model**, a controller (cloud server, app, or user interface) sends **explicit commands** to devices. The device simply executes what it is told, with no autonomy.

**Example: Controlling a Smart Light (Imperative)**

```json
{"command": "turn_on", "device": "light1"}
```

Or, in an RPC-style API:

```json
{"method": "setRGB", "params": {"r": 255, "g": 0, "b": 0}}
```

The device does not make any decisions—it just follows instructions.

**Limitations of the Imperative model**

❌ **No autonomy** – The device does not act on its own.\
❌ **High network dependency** – Every action requires a real-time command.\
❌ **Not scalable** – Managing many devices with direct commands is inefficient.

### **Declarative model: desired state control**

The **declarative model** defines a **goal** or desired state, and the system determines how to achieve it.

**Example: Smart Thermostat (Declarative)**

```json
{"desired_state": {"temperature": 22}}
```

The system ensures that the temperature stays at **22°C**, automatically controlling the heater or fan.

**Limitations of the Declarative model**

❌ **Limited expressiveness** – It only specifies **what** should happen, not **how**.\
❌ **Still requires centralized logic** – The controller interprets and enforces the desired state.\
❌ **Difficult to handle edge cases** – Complex automation rules don’t fit well.

***

## **Why Uniot uses Edge Logic Deployment**

Instead of sending direct commands (**imperative**) or defining a target state (**declarative**), Uniot uses **Edge Logic Deployment**:

✅ **Logic is sent to the device dynamically**\
✅ **The device executes the logic autonomously** via the **Edge Logic Engine**\
✅ **No need for constant network communication**

#### **Example: Smart Thermostat using Edge Logic Deployment**

Instead of sending a one-time command, Uniot deploys **a script** that **runs directly on the device**:

```lisp
(task 0 1000 '
 (if
  (>
   (get_temp) 25)
  (turn_on_ac)
  (print '
   (Temperature is fine! No need to turn on AC))))
```

* The **Edge Logic Engine** on the device **evaluates the condition** in real time.
* If the temperature **exceeds 25°C**, it turns on the AC.
* If not, it **logs a message** instead of executing unnecessary commands.

This means:\
✔ **Devices are autonomous** – they don’t wait for cloud instructions.\
✔ **Network load is reduced** – less traffic from frequent commands.\
✔ **Logic can adapt dynamically** – new scripts can be deployed **without firmware updates**.

### **How Edge Logic Deployment compares to traditional models**

| Feature                   | **Imperative**  | **Declarative** | **Edge Logic Deployment (Uniot)** |
| ------------------------- | --------------- | --------------- | --------------------------------- |
| **Execution Model**       | Direct commands | Desired state   | Scripts run at the edge           |
| **Device Autonomy**       | ❌ No            | ⚠️ Limited      | ✅ Full autonomy                   |
| **Network Dependency**    | ❌ High          | ⚠️ Medium       | ✅ Low                             |
| **Complex Logic Support** | ❌ No            | ⚠️ Limited      | ✅ Yes                             |
| **Real-Time Adaptation**  | ❌ No            | ⚠️ Somewhat     | ✅ Yes                             |
| **Scalability**           | ❌ Hard          | ⚠️ Moderate     | ✅ High                            |

#### **Why this is better**

* **More powerful than declarative models** → Instead of just setting a target state, devices can **execute complex logic**.
* **More flexible than imperative models** → Devices aren’t just passive receivers of commands; they can **react dynamically**.
* **Enables true edge computing** → Instead of relying on the cloud, **logic runs locally** on the **Edge Logic Engine**.

***

## **Why this is not the same as low-level firmware scripting**

A common misunderstanding is that **Edge Logic Deployment** is just a form of low-level scripting, like **Lua on ESP8266** or **MicroPython on microcontrollers**. However, **Uniot’s approach is fundamentally different**.

### **Differences between Edge Logic Deployment and low-level firmware scripting**

| Feature             | **Firmware Scripting (Lua/MicroPython)**       | **Edge Logic Deployment (Uniot)**                        |
| ------------------- | ---------------------------------------------- | -------------------------------------------------------- |
| **Execution Model** | Installed at flash level, runs continuously    | Logic is dynamically deployed and updated                |
| **Update Method**   | Requires full firmware update or manual access | Logic updates are sent over the network                  |
| **Scalability**     | Limited to specific firmware versions          | Any device with an Edge Logic Engine can run new scripts |
| **Device Autonomy** | Requires manual scripting per device           | Centralized deployment, but execution is local           |
| **Flexibility**     | Requires device-specific implementation        | Works across multiple devices without modification       |
| **Security**        | Full access to device internals                | Runs in a controlled environment with restrictions       |

***

### **Key reasons this is different**

✔ **Dynamically deployed:** Unlike MicroPython or Lua, logic is **not hardcoded** – it is deployed at runtime.\
✔ **Works across devices:** The same logic can run on **multiple devices**, without modifying firmware.\
✔ **Security & Control:** The **Edge Logic Engine** runs logic in **a controlled environment**, ensuring **safety**.\
✔ **Uses UniotLisp as a Virtual Machine:** The **Edge Logic Engine** runs [UniotLisp](../advanced/uniot-lisp/), an optimized Lisp-based scripting language, making execution **lightweight, portable, and efficient**.\
✔ **No firmware flashing required:** New logic can be **sent remotely**, unlike firmware scripts that need manual updates.

Instead of treating IoT devices as **programmable boards** (like Arduino with MicroPython), **Uniot treats them as smart agents that receive and execute logic dynamically**.

***

## **Conclusion: Edge Logic Deployment is the Future**

By **sending scripts instead of commands or states**, Uniot enables **true edge computing** where devices:

* **Execute autonomous logic locally**
* **Adapt dynamically to real-world conditions**
* **Require less cloud dependency**
* **Scale easily to large networks**

This shift from **command-driven control** to **dynamic logic deployment** is a **game-changer** in IoT, edge computing, and automation.
