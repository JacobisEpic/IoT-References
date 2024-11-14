# Tomato Router

If you are using the campus network or a home router, these
instructions will be approximate. The concepts are the same but the
menus are different.

We have two types of routers used in the
class: the WRT54GS/GL and the E1200 v2. The older WRT54 model is set
up to use firmware called "Tomato" v1.28. Upgrades from this version
are unlikely due to memory limitations on the hardware.

The E1200 v2 routers are new and run the out-of-box linksys
software. You will update these with a different thread of open source
Tomato software. This is all new. The interfaces will be "similar."

In summary:

- WRT54GS/GL: [Polarcloud Tomato](http://www.polarcloud.com/tomato)
  - Tomato_1_28.7
- E1200 v2: [Tomato by Shibby](http://tomato.groov.pl/?page_id=81)
  - [Router list](http://tomato.groov.pl/?page_id=69)
  - [E1200 v2 Firmware](http://tomato.groov.pl/download/K26RT-N/build5x-140-MultiWAN/Linksys%20E-series/tomato-E1200v2-NVRAM64K-1.28.RT-N5x-MIPSR2-140-Max.zip)


This skill is intended to familiarize you with the router and Tomato
firmware.

<p align="center">
<img src="/docs/images/wrt54g.jpg" width="30%">
<img src="/docs/images/e1200v2.jpg" width="30%">
</p>
<p align="center">
<i> Linksys WRT54GS and E1200 v2 Routers</i>
</p>

## Assignment 0: Reset & check your router
1. Find the instructions online to reset your router to "factory defaults"
2. After reset, login to the router's web interface (likely with http://192.168.1.1 and UID root PWD admin)
3. See if it is already running the Tomato firmware...if so, skip Assignment 1 and go directly to Assignment 2 below


## Assignment 1: Reflash your router
1. Download to your laptop the latest version of the Tomato firmware based on your router type WRT54GL or E1200 v2
2. Plug the WAN port of the router to a hot upstream ethernet port
3. Connect your laptop into one of the LAN ports on the router
4. Plug in and reset the router (hold reset button for 30s)
5. Log in to the router (http://192.168.1.1 with UID root PWD admin)
6. Find the adminstration tab, then button for updating firmware
7. Follow the instructions, locating the saved firmware file from your laptop
8. Reboots... log in again


## Assignment 2: Set up your router
1. Log in to the router (http://192.168.1.1 with UID root PWD admin)
2. Under Basic
   - DHCP server should be 'on'
   - Change SSID to match the label on your router 'Group_X'
   - Set security to ~~WPA Personal~~ WPA2 (required for ESP32 Station example code)
   - Set shared key to be 'smartsys'
   - Set channel based on your [team #](/docs/utilities/docs/wifi-channels.md)
   - Save settings
3. Under Basic/Identification
   - Give your router a name 'Group_X'
   - Save settings
4. Under Basic/Time
   - Set time zone
   - Set NTP server
   - Save  
5. Under Basic/DDNS
   - Setup Dynamic DNS as per (separate step later)
   - Save
6. Under Administration
   - Update password to: 'smart'
   - Save and reboot
8. Explore the device list and other data reporting features
9. Report.md

***If you have one of the newer routers, you will have to click around to find similar configuration tabs as the Tomato 
version will be different.***


## Reference material
- [Tomato](http://www.polarcloud.com/tomato)
- [Tomato by Shibby](http://tomato.groov.pl/?page_id=81)
- [WiFi Channel Assignments](/docs/utilities/docs/wifi-channels.md)
- [openWRT for Linksys WRT54GS](https://openwrt.org/toh/linksys/wrt54g)
