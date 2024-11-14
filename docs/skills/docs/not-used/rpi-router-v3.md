# Using the Raspberri Pi as a Router

## Udpate -- this skill can be satisfied by using a regular router instead of the pi

(Reiterated here from the Piazza post) Due to the multiple issues with
the pi router, I am relaxing this assignment in favor of alternatives.
Set up your router

1. ***Issue:*** Can't get Pi working as router
   - ***Solution:*** use borrowed router or access home router control panel to set up DDNS and port forwarding.
2. ***Issue:*** Can't set up DDNS or port forwarding on home router and I can't get one of the loaners
   - ***Solution:*** demonstrate DDNS with a team member, with port forwarding on the other end
3. See [Router Setup](/docs/skills/docs/router.md)

Also, the DDNS skill is now a team skill (can share the results). 

-----

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
card, so be sure your pi is configured and bootable (separate skill).
The files listed in the instructions above can be found in the folder
**/boot** on your running Pi.*

Follow the instructions in "**Step 1**" only, and stop after the
"**SSH**" section. Do NOT take the steps in the "Advanced Networking"
section (this will prevent your Pi from working as a router).

<a name="Step2"/>

### 2. Enable "connection sharing"
Now that your pi is connected to your computer as an ethernet device
it can share your Internet connection over the USB cable.

The steps to enable connection sharing are OS-specific. Generic
[Windows](#Windows), [Mac OS](#MacOS), and [Linux](#Linux)
instructions are listed below. If these don't work for you, head to
Google/Bing/DuckDuckGo and start searching...

**Note:** After booting/rebooting your Pi you *may periodically* need
  to disable and re-enable connection sharing on your computer - keep
  these instructions handy.

<a name="Windows"/>

#### Windows 

See general instructions here: [RASPBERRY PI ZERO USB/ETHERNET GADGET
TUTORIAL](https://www.circuitbasics.com/raspberry-pi-zero-ethernet-gadget/)

NOTE FOR ABOVE:

 - Jump to section "**SETTING UP SHARED INTERNET ACCESS**", ignoring the first few sections (they're a little outdated).  

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

1. SSH into your Pi using the USB "raspberrypi.local" connection setup above (i.e., not the WiFi connection you configured in a previous skill).
2. Install the access point and network management software on your Pi:
	- Install the access point software:
		* `sudo apt install hostapd`
	- Enable the wireless access point service and set it to start when your Pi boots: 
		* `sudo systemctl unmask hostapd`
		* `sudo systemctl enable hostapd`
	- Install DNS/DHCP software:
		* `sudo apt install dnsmasq`
	- Install utilities to enable wireless devices to route through your Pi (below is all one line):
		* `sudo DEBIAN_FRONTEND=noninteractive apt install -y netfilter-persistent iptables-persistent` 
3.   Setup the wireless interface for routing:
		- `sudo nano /etc/dhcpcd.conf`
		- Add the following to the end of the file and save it:
			```
			interface wlan0
		        static ip_address=192.168.2.1/24
		        nohook wpa_supplicant
			```
4. Enable IP routing and masquerading:
	-	`sudo nano /etc/sysctl.d/routed-ap.conf`
	-	Verify the file has the following contents (or add them) and save it:
	    ```
	    # Enable IPv4 routing
	    net.ipv4.ip_forward=1
	    ```
	 - Configure a firewall rule:
		 * `sudo iptables -t nat -A POSTROUTING -o usb0 -j MASQUERADE`
	 - And set it to load at boot:
		 * `sudo netfilter-persistent save`
5. Configure DHCP and DNS:
	- `sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig`
	- `sudo nano /etc/dnsmasq.conf`
	- Add the following to the file and save it:
		```
		interface=wlan0   # Listening interface
		dhcp-range=192.168.2.2,192.168.2.200,255.255.255.0,24h
		domain=wlan   # Local wireless DNS domain
		address=/gw.wlan/192.168.2.1   # Alias for this router
		```
6.  Configure the wireless radio and accesspoint:
	 - `sudo rfkill unblock wlan`
	 - `sudo nano /etc/hostapd/hostapd.conf`
	 - Add the following to the file and save it (setting channel and ssid based on your team information as outlined below):
	    ```
	   	country_code=US
	   	interface=wlan0
	   	ssid=Group01
	   	hw_mode=g
	   	channel=7
	   	macaddr_acl=0
	   	auth_algs=1
	   	ignore_broadcast_ssid=0
	   	wpa=2
	   	wpa_passphrase=smartsys
	   	wpa_key_mgmt=WPA-PSK
	   	wpa_pairwise=TKIP
	   	rsn_pairwise=CCMP
    	```
7. Reboot and you should now be able to connect to your new wireless access point!
	 -   `sudo systemctl reboot`

NOTE FOR ABOVE:

 - You will be using the "Ethernet Gadget" connection over USB as the connection to the Internet.
 - You will use the pi's built-in Wi-Fi for the "private network"
 - Meaning there is no "USB Wi-Fi adapter" needed for this setup

The components to install are: (1) hostapd -- a hotspot deamon
(service) and (2) dnsmasq -- a DNCP and DNS server.

Use the 192.168.1.1 as the wlan0 interface

Set the dhcp range as
dhcp-range=192.168.1.2, 192.168.168.1.200, 255.255.255.0,24h

Set hostapd configuration as per instructions, but with the following changes:

ssid=Group01
wpa_passphrase=smart

Follow the rest of the instructions, except "2. Wireless interface names" (this can be ignored).  


The configuration that we seek is the following:

- "Router" IP address (WAN side) assigned by DHCP of your laptop/desktop computer
- Local subnet of 192.168.1.1 
- Enable local DHCP server
- Set SSID to your group number, such as 'Group01'
- Set security to WPA Personal
- Set shared key to be 'smartsys'  *(must be between 8 and 20 characters!)*
- Set channel based on your [team #](/docs/utilities/docs/wifi-channels)
- Enable NTP server (separate skill)
- Enable Dynamic DNS as per (separate skill)


## Lessons Learned
- You must re-flash your Raspberry Pi without a wpa_supplicant.conf file before following the directions in the skill to get the router running.
To recap: DO NOT SET UP A WPA_SUPPLICANT.CONF file for this skill.


## Assignment
1. Bring up the pi as the AP
2. Demonstrate that it works
3. Report

## Reference Material
- [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
- [Ethernet Gadget](https://learn.adafruit.com/turning-your-raspberry-pi-zero-into-a-usb-gadget/ethernet-gadget)
- [WiFi Channel Assignments](/docs/utilities/docs/wifi-channels.md)
- [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/)
