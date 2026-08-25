---
hidden: true
---

# Device Network

Your Uniot device needs an Internet connection to communicate with the platform. The [WiFi Management](../advanced/uniot-core.md#wifi-management) subsystem of Uniot Core handles all network connectivity.

## Network Configuration

Configure the network in your `setup()` function:

{% code title="main.cpp" %}

```c++
void setup() {
  // ... other setup code ...

  MainAppKit.configureNetworkController({
    .pinBtn = PIN_BUTTON,
    .activeLevelBtn = BTN_PIN_LEVEL,
    .pinLed = PIN_LED,
    .activeLevelLed = LED_PIN_LEVEL,
    .maxRebootCount = 255
  });

  // ... other setup code ...
}
```

{% endcode %}

See [WiFi Management](../advanced/uniot-core.md#wifi-management) for detailed parameter descriptions.

## Status Indication

If your device has an LED, you can use LED indication to define different network states through blink patterns:

| Pattern                        | Meaning    | Description                               |
| ------------------------------ | ---------- | ----------------------------------------- |
| Slow blink (≈0.5 blinks/sec)   | Standby    | Access Point mode, waiting for WiFi setup |
| Medium blink (≈1 blink/sec)    | Connecting | Attempting to connect to configured WiFi  |
| Fast blink (≈2.5 blinks/sec)   | Error      | Connection failed or other error          |
| Off                            | Connected  | Normal operation, connected to WiFi       |

## Network Control

If your device has a button, you can use it to manage the network:

### Reconnect to WiFi

- Hold the button for ~3 seconds
- Use when device disconnects and enters Access Point mode
- Attempts to reconnect to previously configured network

### Reset WiFi Settings

- Quick-press 4 or more times, then hold for ~3 seconds (complete the whole sequence within ~5 seconds of the first press)
- Clears current WiFi configuration
- Enters Access Point mode for new network setup

## Common Issues

1. **Device Won't Connect**

   - Verify WiFi credentials
   - Check signal strength
   - Ensure network compatibility

2. **Frequent Disconnections**

   - Improve signal strength
   - Check power supply stability
   - Verify network stability

3. **Can't Enter Setup Mode**
   - Try power cycling the device
   - Check button connections
   - Verify firmware version
