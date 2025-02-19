# Device Network

Your Uniot device needs an Internet connection to communicate with the platform. The [Network](../advanced/uniot-core/network/README.md) module handles all network connectivity.

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

See [NetworkController](../advanced/uniot-core/network/networkcontroller.md) for detailed parameter descriptions.

## Status Indication

If your device has an LED, you can use LED indication to define different network states through blink patterns:

| Pattern | Meaning | Description |
|---------|---------|-------------|
| 1 blink/sec | Standby | Access Point mode, waiting for WiFi setup |
| 2 blinks/sec | Connecting | Attempting to connect to configured WiFi |
| 5 blinks/sec | Error | Connection failed or other error |

## Network Control

If your device has a button, you can use it to manage the network:

### Reconnect to WiFi

- Long press (3-5 seconds)
- Use when device disconnects and enters Access Point mode
- Attempts to reconnect to previously configured network

### Reset WiFi Settings

- Quick press 5-8 times, then hold 3-5 seconds
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
