# Using the Raspberri Pi as a Router

This skill assumes that you have already installed software on the pi
and have established that you can log in and connect the pi to the
internet for software updates.

In this skill you will install software to enable the pi (Pi Zero W --
Wireless) to operate as a WiFi router. This implies that the pi will
host an WiFi access point to allow you to have a local subnet for your
wireless devices (e.g., your laptop, ESP32s, and any other WiFi
devices).  We use this approach as many of you will not have access to
fully control the network access features of your local router (e.g.,
campus router, or home router).

<center><img src="/docs/images/rpi-router.jpg" width="80%" /></center>
<center> RPi Zero used as a Wireless AP/Router</center>

We are using open source software here -- please bear with the
gaps. 

Follow the instructions here: [RPi as Wireless AP](https://thepi.io/how-to-use-your-raspberry-pi-as-a-wireless-access-point/)

The components to install are: (1) hostapd -- a hotspot deamon
(service) and (2) dnsmasq -- a DNCP and DNS server.

Use the 192.168.1.1 as the wlan0 interface

Set the dhcp range as
dhcp-range=192.168.1.2, 192.168.168.1.200, 255.255.255.0,24h

Set hostapd configuration as per instructions, but with the following changes:

ssid=Group01
wpa_passphrase=smart

Follow the rest of the instructions.


The configuration that we seek is the following:

- Router IP address (WAN side) assigned by DHCP of your local internet provider (BU, Comcast, Verizon, etc.).
- Local subnet of 192.168.1.1 
- Enable local DHCP server
- Set SSID to your group number, such as 'Group01'
- Set security to WPA Personal
- Set shared key to be 'smart'
- Set channel based on your [team #](/docs/utilities/docs/wifi-channels.md)
- Give your router a name, such as 'Group01'
- Set time zone
- Enable NTP server
- Enable Dynamic DNS as per (separate skill)



## Assignment
1. Bring up the pi as the AP
2. Demonstrate that it works
3. Report

## Reference Material
- [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
- [Setting up Pi as Wireless AP](https://thepi.io/how-to-use-your-raspberry-pi-as-a-wireless-access-point/)
- [WiFi Channel Assignments](/docs/utilities/docs/wifi-channels.md)
- [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/)
