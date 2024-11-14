# Tomato Router

If you are using the campus network or a home router, these
instructions will be approximate. The concepts are the same but the
menus are different.

We have two types of routers used in the class: the WRT54GS/GL and the
E1200 v2. The older WRT54 model may have older router software and
must be upgraded.

Most recent firmware is here:
- WRT54GS/GL: [Fresh Tomato](https://freshtomato.org/downloads/freshtomato-mips/2023/2023.1/K26/freshtomato-K26-NVRAM32K_RT-MIPSR2-2023.1-Mini.zip) latest version 2/2023
- E1200 v2: [Fresh Tomato](https://freshtomato.org/downloads/freshtomato-mips/2023/2023.1/K26RT-N/Linksys%20E-series/freshtomato-E1200v2-NVRAM64K_RT-N5x-MIPSR2-2023.1-Max.zip) latest version 2/2023

This skill is intended to familiarize you with the router and Tomato
firmware.

<p align="center">
<img src="/docs/images/wrt54g.jpg" width="30%">
<img src="/docs/images/e1200v2.jpg" width="30%">
</p>
<p align="center">
<i> Linksys WRT54GS and E1200 v2 Routers</i>
</p>

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


## Reference material
- [Fresh Tomato](http://freshtomato.org)
- [WiFi Channel Assignments](/docs/utilities/docs/wifi-channels.md)
- [openWRT for Linksys WRT54GS -- not used](https://openwrt.org/toh/linksys/wrt54g)
- [Tomato -- legacy](http://www.polarcloud.com/tomato)
