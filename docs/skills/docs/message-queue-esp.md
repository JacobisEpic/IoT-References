# WiFi

WiFi was introduced back in the '90s as a wireless LAN (WaveLAN)
through development efforts of NCR and AT@T. The rebranded AT&T
(Lucent) made some of the first commercially available cards called
ORiNOCO that operated at the base rate of 11Mb/s. Apple Computer adopted this
technology in the early 2000s and this was one of the catalysts for
its proliferation.

WiFi (802.11) is no longer one thing, but a collection of evolving
standards. It's a moving target. But for the purpose of
interconnecting wireless devices, it has some excellent and not-so
excellent properties. It is defined as a WLAN (wireless local area network)
technology as opposed to a WPAN (wireless personal area network)
technology. This differentiates it from, for example, bluetooth, zigbee, or
near-field communications technology (card readers).

## Properties

- 2.4 GHz and 5 GHz bands
- ~150 m range
- Data rates in excess of 1 Gb/s under some operating conditions
- Higher power consumption that some WPAN technologies
- Shared medium can result in unpredictable latency due to random backoff contention protocol 
- Congestion is possible

<p align="center">
<img src="/docs/images/wifi.png" width="30%">
</p>
<p align="center">
<i> WiFi, from Wikimedia Commons</i>
</p>

What is remarkable is how much WiFi technology has matured for
it to be embedded into products like the ESP32 with relatively low
power consumption. It is now at the point that it can be competitive
with other technologies such as BLE which has been designed
specifically for embedded low power devices.

In this assignment your task is to bring up the basic WiFi
functionality on the ESP32.  We recommend completing the router
configuration skill prior to this skill.

## Note
- The ESP32 WiFi Station example code uses WPA2 -- you may need to
check your router configutation to make sure it is set to match this
type of security access.


## Assignment
1. Make sure you have the latest ESP32 files
2. Find the wifi area and download (or go to your local repo) the WiFi 
Station example. A 'station' here means a mobile device vs. an access point. The repo was most recently found here: [ESP32 WiFi Station Example](https://github.com/espressif/esp-idf/tree/master/examples/wifi/getting_started/station).
3. Build and flash this example using the specs for your team's AP (SSID and access credentials)
4. If successful, your ESP32 should be assigned an IP address
5. Go to the router admin page, under Status and open the Device List to see if your ESP32 is on the network
6. You now have successfully established the ESP32 on the WiFi LAN
7. Report

## Reference material
- [WiFi Channel Assignments](/docs/utilities/docs/wifi-channels.md) -- only if these were set before, otherwise leave as-is (dynamically selected)

