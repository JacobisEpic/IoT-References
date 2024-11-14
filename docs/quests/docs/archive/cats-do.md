# What Do Cats Do When No One is Watching?

<p align="center">
<img src="/docs/images/things.png" width="80%">
</p>
<p align="center">
<i>Things 1 and 2</i>
</p>

We have two cats at home. On the weekends when we are home we see that
one mostly sleeps and the other tears around causing trouble. But what
happens when we are away? This quest is to build a system to find
out. We'll use a temperature sensor in the favorite sleeping spot to
quantify sleeping habits, an accelerometer to find out how much they
move around, a toy to entertain them, and a web camera to peek in to
the house to see them eating. We also want some form of data playback
to check in at specific moments in the data stream, for example, to
find out which cat has been naughty. We'll call this system "Cat
Tracker."

<p align="center">
<img src="/docs/images/cat-tracker.png" width="80%">
</p>
<p align="center">
<i>Cat Tracker Components</i>
</p>

 
## Description

The key features of Cat Tracker are:
- Measurement of temperature to determine occupancy in sleeping location (ESP-1)
- Active movement using acceleration (of sensor on collar) (ESP-2)
- Flashing of LEDs or buzzer to entertain cat (ESP-3)
- Webcam sourcing video, embedded in a single portal window
- Data sent from ESP32 sensors over WiFi 
- Remote access through a portal to display data in real-time data at remote client
- Remote access through a portal to control LEDs and to configure features at a remote client


A big portion of this quest is wireless connectivity and remote
access.

<p align="center">
<img src="/docs/images/cat-sol.png" width="80%">
</p>
<p align="center">
<i>Cat Tracker System Overview</i>
</p>

As with other quests, there are a number of moving parts, but each part
is not as complex as it sounds. We approach this problem with the
following breakdown:

1. Bring up your code for peripherals (LEDs, accellerometer, thermistor, timers). Make sure they work before you integrate with other items.
2. Configure your Rpi for remote access (DDNS) -- this can be a unique IP address
3. Get the ESP32s to work with your WiFi access point to establish connectivity
4. Establish how you will transfer data from the ESP32s to a web client or server. We
recommend using the UDP protocol.
5. Integrate control of the LED over your local network
6. Design the web client (portal) to provide control. We recommend doing this via a 
local node.js server with calls to your ESP32s, which makes the location of your 
hosting server independent of where your web client is located.
7. It may be easiest to develop one code base for the ESP32s and to deploy on each of the three units used

*The above is a recommendation but there are certainly different ways of doing this.*

## Solution Requirements
- Must be able to control the LED/buzzer from a remote interface (simple on/off is fine, or vary intensity)
- Must show accurate status report of temperature, (acceleration is optional), in real-time at remote client in strip-chart or equivalent way, using a web browser. No graph scrunching -- fixed time window for displayed data.
- Must stream video from RPi

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
<!---
4. Investigative question: What are steps you can take to make your device and system low power? Please cite sources for you answer.
--->

## Tips
- The client browser should be on an external network (e.g., home network or campus network)
- Your router runs DDNS and port forwards to your node.js server. Put the RPi and ESP32s on a site where you can access the DDNS configuration for your router (a router will be provided)
- Setup your node.js server (laptop) with static IP (assigns same subnet IP every time to MAC address of your laptop). Your tomato router will do this for you
- Node.js server goes on the local subnet and talks to the ESP32
- ESP32s are on the subnet of your router and talk to the node.js sever
- Setup ESP32s with static IPs on subnet (as per MAC address). Static IP address assignment by MAC is configured in Devices tab of router.
- ***It will be very difficult to debug a system brought up all at once.*** You need to test the individual parts first
- The skill assignments represent the individual parts -- make these work first
- Test your networking pieces on the local network first, then add the remote parts (it won't work remotely if it does not work locally)
- Build your node server on your laptop first; make sure it works, then port to the RPi
- Also, it is possible to host multiple http (web) servers on the pi
  - One URL/port for camera
  - One inside node server


## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Uses multiple ESP; one for acceleration (optional), one for temperature, and one for LED control |  |  1     | 
| Displays real-time data (temperature, accelleration) at remote client via portal using separate IP network |  |  1     | 
| Able to scroll past data in display |  |  1     | 
| Controls LEDs on ESP from remote client via portal |  |  1     |  
| Sources web cam video into remote client |  |  1     | 
| ESPs and RPi are connected wirelessly to router; ESP32 sensor data are delivered to local node server (on local laptop or RPi) |  |  1     | 



## Reference material
- [WiFi Station Example](https://github.com/espressif/esp-idf/tree/master/examples/wifi/getting_started/station)
- [UDP client](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sockets/udp_client)
