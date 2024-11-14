# IoT Provisioning

A new IoT device will have no knowledge of the existing wireless
infrastructure (SSID, username, passwords), nor will it have any
security. During provisioning it will be vulnerable to other parties
taking ownership. Therefore, when provisioning a new IoT device,
router/WiFi credentials need to be somehow provided to the IoT device
before the device can connect to the network.

In this exercise, you will implement the ESP32 in two different
states: a "soft AP" mode and a station mode. In soft AP mode, the ESP32
will set itself up as an access point (AP) and await connections from other
devices to provide it with router/WiFi credentials. In station mode,
the ESP32 will connect to your router. Your solution should enable
seamless transitions between these two states.

<p align="center">
<img src="/docs/images/provision.png" width="80%">
</p>
<p align="center">
<i>Provisioning</i>
</p>

## Assignment
1. Demonstrate IoT Provisioning
   - New device mode in soft AP mode
   - Connect to ESP32 from your laptop
   - Provide router credentials to ESP32 from laptop
   - ESP32 connects to router in station mode
   - Power off router, i.e., router is disconnected
   - ESP32 reverts to soft AP mode
2. Button press to revert to soft AP mode
3. Optional, remote user input in station mode to revert to soft AP mode
4. Report

## Reference material
- [ESP32: WiFi](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/wifi/esp_wifi.html)
- [WiFi Examples](https://github.com/espressif/esp-idf/tree/bd90f53/examples/wifi)
