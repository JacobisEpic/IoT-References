# BLE

BLE stands for ‘bluetooth low energy.” It’s a version that improves
the energy consumption properties of bluetooth. For ESP32, we will use
the BT&BLE dual-mode bluetooth.

In this exercise we will configure and run the BLE on the ESP32 in
anticipation of applications that best exploit a WPAN rather than a
WLAN (WiFi).

<p align="center">
<img src="/docs/images/ble.jpg" width="50%">
</p>
<p align="center">
<i> Bluetooth Low Energy</i>
</p>

The Serial Port Profile (SPP) defines the requirements for Bluetooth
devices necessary for setting up emulated serial cable connections
using RFCOMM between two peer devices. The requirements are expressed
in terms of services provided to applications, and by defining the
features and procedures that are required for interoperability between
Bluetooth devices.

Essentially, the Serial Port Profile defines the protocols and
procedures that shall be used by devices using Bluetooth for RS232 (or
similar) serial cable emulation.The scenario covered by this profile
deals with legacy applications using Bluetooth as a cable replacement,
through a virtual serial port abstraction (which in itself is
operating system-dependent).

## Step by Step Guide
1. Overall process using ESP_APIs to create SPP initiator and acceptor
2. Set up the device name and set up the mode
3. Start up searching the classic devices
4. Connect the device through other devices (ESP32 or laptop)
5. Once the connection is established, send the data through SPP
6. Print out the data via bluetooth serial port

## Assignment
1. Get the demo to work
2. Report

## Reference material

- [Dual-Mode Bluetooth](https://www.espressif.com/sites/default/files/documentation/btble_coexistence_demo_en.pdf)
- [SPP Initializer](https://github.com/espressif/esp-idf/tree/master/examples/bluetooth/bt_spp_initiator)
- [SPP Accepter](https://github.com/espressif/esp-idf/tree/master/examples/bluetooth/bt_spp_acceptor)
- [Bluetooth Serial Port](https://apple.stackexchange.com/questions/169437/bluetooth-serial-port-profile-spp-support-in-os-x-yosemite)
- [ESP32 Github: Bluetooth Examples](https://github.com/espressif/esp-idf/blob/51a4b4ba2716e7b57aeafa804c48f927d8d3895a/examples/bluetooth/README.md)
- [ESP: Bluetooth API](https://esp-idf.readthedocs.io/en/latest/api-reference/bluetooth/index.html)
