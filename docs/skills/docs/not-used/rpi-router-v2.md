# Using the Raspberri Pi as a Router

This skill assumes that you have already installed software on the pi
and have established that you can log in and connect the pi to the
internet for software updates.

In this skill you will install software to enable the pi (Pi Zero W
--Wireless) to operate as a WiFi router. This implies that the pi will
host a WiFi access point to allow you to have a local subnet for your
wireless devices (e.g., ESP32s and any other WiFi devices).  We use
this approach as many of you will not have access to fully control the
network access features of your local router (e.g., campus router, or
home router).

<center><img src="/docs/images/rpi-router.jpg" width="80%" /></center>
<center> RPi Zero used as a Wireless AP/Router</center>

We are using open source software here -- please bear with the gaps. 

There are 3 steps / components to this process: 

 1. [Enable "Ethernet Gadget" mode for the pi connected to your laptop/desktop computer](#Step1)
 2. [Enable "connection sharing" to allow the pi to access the Internet through your computer](#Step2)
 3. [Configure the pi as a Wireless Access Point](#Step3)

<a name="Step1"/>

### 1. Enable "Ethernet Gadget"
Follow the Adafruit instructions here: [Ethernet
Gadget](https://learn.adafruit.com/turning-your-raspberry-pi-zero-into-a-usb-gadget/ethernet-gadget)

*You will be making changes to the configuration files on the pi's SD
 card, so be sure your pi is configured and bootable (separate
 skill).*

Follow the instructions in "**Step 1**" only, and stop after the
"**SSH**" section.

<a name="Step2"/>

### 2. Enable "connection sharing"
Now that your pi is connected to your computer as an ethernet device
it can share your Internet connection over the USB cable.

The steps to enable connection sharing are OS-specific. Generic
[Windows](#Windows), [Mac OS](#MacOS), and [Linux](#Linux)
instructions are listed below. If these don't work for you, head to
Google/Bing/DuckDuckGo and start searching...

<a name="Windows"/>

#### Windows 

See general instructions here: [RASPBERRY PI ZERO USB/ETHERNET GADGET
TUTORIAL](https://www.circuitbasics.com/raspberry-pi-zero-ethernet-gadget/)

NOTE FOR ABOVE:

 - Jump to section "**SETTING UP SHARED INTERNET ACCESS**", ignoring
   the first few sections (they're a little outdated).

<center><img src="/docs/images/rpi-router-win-shared.png" width="80%" /></center>

<a name="MacOS"/>

#### Mac OS
*Instructions courtesy [Share Internet Between macOS and a Raspberry
 Pi Zero Over
 USB](https://www.thepolyglotdeveloper.com/2019/07/share-internet-between-macos-raspberry-pi-zero-over-usb/)*

> Go to the  **System Preferences**  on your Mac and choose the 
> **Sharing**  option. We need to configure  **Internet Sharing**  within this area.  
> 
> ...choose the device that you’d like to share your internet with. In
> our scenario, we have an Ethernet gadget, which is the Raspberry Pi
> Zero emulating Ethernet over USB. After selecting the device, don’t
> forget to enable internet sharing in general. There should be two
> boxes checked in total, and after you’ll get a confirmation dialog.  
> 
> You may need to restart your Raspberry Pi after enabling internet
> sharing between your host computer and the device.

![enter image description here](https://www.thepolyglotdeveloper.com/uploads/2019/07/macos-internet-sharing.png)

<a name="Linux"/>

#### Linux

See general instructions here: [How to Share Wired Internet Via Wi-Fi
and Vice Versa on
Linux](https://www.tecmint.com/share-internet-in-linux/)

NOTES FOR ABOVE:

 - The "second computer" will be your pi connected via USB cable as an ethernet device. 
 - Jump to section "**Sharing Wi-Fi Internet Connection via Wired(Ethernet) Connection**", ignoring the first section.
 - The "**Wired/Ethernet connection**" will be the pi device connected to your computer.

<a name="Step3"/>

### 3. Configure the pi as a Wireless Access Point

Follow the directions here: [Creating Wireless Router using Raspberry
Pi Zero
W](https://scribles.net/creating-wireless-router-using-raspberry-pi-zero-w/)

NOTE FOR ABOVE:

 - You will be using the "Ethernet Gadget" connection over USB as the connection to the Internet.
 - You will use the pi's built-in Wi-Fi for the "private network"
 - Meaning there is no "USB Wi-Fi adapter" needed for this setup

The components to install are: (1) hostapd -- a hotspot deamon
(service) and (2) dnsmasq -- a DNCP and DNS server.

- Use the 192.168.2.1 as the wlan0 interface
- Set the dhcp range as
dhcp-range=192.168.2.2, 192.168.2.200, 255.255.255.0,24h
- Set hostapd configuration as per instructions, but with the following changes:

  - ssid=Group01
  - wpa_passphrase=smart
- Follow the rest of the instructions, except "2. Wireless interface names" (this can be ignored).  


Ultimately this leads to the following configuration that we would want on any router (if you happen to have
an accessible one): 

- "Router" IP address (WAN side) assigned by DHCP of your laptop/desktop computer
- Local subnet of 192.168.2.1 
- Enable local DHCP server
- Set SSID to your group number, such as 'Group01'
- Set security to WPA Personal
- Set shared key to be 'smart'
- Set channel based on your [team #](/docs/utilities/docs/wifi-channels)
- Enable NTP server (separate skill)
- Enable Dynamic DNS as per (separate skill)



## Assignment
1. Bring up the pi as the AP
2. Demonstrate that it works
3. Report

## Reference Material
- [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
- [Ethernet Gadget](https://learn.adafruit.com/turning-your-raspberry-pi-zero-into-a-usb-gadget/ethernet-gadget)
- [Creating Wireless Router using Raspberry Pi Zero W](https://scribles.net/creating-wireless-router-using-raspberry-pi-zero-w/)
- [WiFi Channel Assignments](/docs/utilities/docs/wifi-channels)
- [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/)
