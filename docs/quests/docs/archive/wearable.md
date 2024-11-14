# Wearable Computing

This quest is to build an instance of a wearable device that records
biometrics and reports back to a central graphical hub.

## Description

<p align="center">
<img src="/docs/images/wearable.png" width="100%" />
</p>
<p align="center">
<i> Smart Appliance Scenario</i>
</p>


The key features of the wearable are going to be:
- Measurements for step, body temperature, and battery level
- Regularly scheduled alerts [to drink water] (blinks blue LED)
- An online portal displaying a real-time status report
- Ability to find your device from web portal (blinks red LED)
- Remote access to turn off features (i.e., only measure steps but no temperature) and view the portal

This basically translates to a barebones fitness watch, which monitors
your health and encourages healthy habits. A big portion of this quest
is also **wireless connectivity** and **remote access**. So to make it
interesting, you want to be able to access your information from any
web portal so your friends and family can follow along. You also want
to program the wearable functions (alerts) from a remote client.

As with all of these assignments, there are a lot of moving parts, but
each part is not as complex as it sounds. We approach this problem
with the following breakdown:

1. Bring up your peripherals (LEDs, vibration switch, thermistor, timers)
2. Configure your router -- test remote access (DDNS)
3. Get the ESP32 to "talk" to a WiFi access point to establish connectivity
4. Establish how you will transfer data from the ESP32 to a web client
or server (could be colocated on your laptop). We are recommending UDP protocol.
5. Integrate control of the peripherals over your local network
6. Design the web client (page) to provide control. We recommend doing this via a local node.js server with calls to your ESP32, which makes the location of your hosting server independent of your laptop (when we move this to the RPi later). Alternatively your can write javascript at your client.

*The above is a recommendation but there are certainly different ways of doing this.*

Here is an illustration of the basic strategy:

<p align="center">
<img src="/docs/images/wearable-strategy.png" width="100%" />
</p>
<p align="center">
<i> Strategy Overview</i>
</p>

## Solution Requirements
- Must be able to control wearable from a remote interface
- Must be able to program 2 alerts (scheduled and instant) remotely
- Must show accurate status report of wearable metrics (step, temperature, and battery level) in real-time at remote client

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: What are steps you can take to make your device and system low power? Please cite sources for you answer.


## Tips
- Client browser is on an external network (e.g., home network or campus network)
- Your router runs DDNS and port forwards to your node.js server
- Setup your node.js server (laptop) with static IP (assigns same subnet IP every time to MAC address of your laptop)
- Node.js server is on the local subnet and talks to the ESP32
- ESP32 is on the subnet of your router and talks to the node.js sever
- Setup ESP32 with static IP on subnet (as per MAC address). Static IP address assignment by MAC is configured in Devices tab of router.

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Does A  |  |  1     | |
| Does B  |  |  1     | |
| Does C  |  |  1     | |
| Does D  |  |  1     | |
| Does E  |  |  1     | |
| Does F  |  |  1     | |
| Does G  |  |  1     | |
