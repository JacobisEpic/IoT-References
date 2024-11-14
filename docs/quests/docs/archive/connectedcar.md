# Connected Car

In this quest we will sensorize a car and connect it to a
network. This can be useful in cases where remote person (e.g., in
case of an accident or need of assistance) may wish to see the state
of the occpuants or their surroundings. Recording this information can
also have benefits, e.g., for insurance purposes.  Similar to smart
vehicles today, our device would make recordings based on what you
have in the course kit.

<p align="center">
<img src="/docs/images/ccar.jpg" width="80%" />
</p>
<p align="center">
<i> Connected Car</i>
</p>

## Description

The key features of the connected car are:
- Measurements temperature, acceleration, and possibly other values (such as battery level)
- Data sent from ESP32 sensors over WiFi 
- Remote access through a portal to display a real-time data at remote client, in graphical form (stripchart with fixed time series window)
- Remote access through a portal (by portal we mean a web site) to control LEDs and to configure features at a remote client
- Webcam sourcing video, embedded in a single portal window

A big portion of this quest is also wireless connectivity and remote
access.

As with all of these assignments, there are a lot of moving parts, but
each part is not as complex as it sounds. We approach this problem
with the following breakdown:

1. Bring up your peripherals (LEDs, accellerometer, thermistor, timers). Make sure they work before you integrate with other items.
2. Configure your pi for remote access (DDNS) -- this can be a unique IP address
3. Get the ESP32 to "talk" to a WiFi access point to establish connectivity
4. Establish how you will transfer data from the ESP32 to a web client or server (could be colocated on your laptop). We are recommending UDP protocol.
5. Integrate control of the LED over your local network
6. Design the web client (page) to provide control. We recommend doing this via a 
local node.js server with calls to your ESP32, which makes the location of your 
hosting server independent of your laptop (when you move this to the RPi later). Alternatively your can write javascript at your client.

*The above is a recommendation but there are certainly different ways of doing this.*

## Solution Requirements
- Must be able to control the alert LED from a remote interface (simple on/off is fine, or vary intensity)
- Must show accurate status report of temperature, vibration, battery level in real-time at remote client in strip-chart or equivalent way, using a web browser. No graph scrunching -- fixed time window for displayed data.

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: What are steps you can take to make your device and system low power? Please cite sources for you answer.


## Tips
- Client browser is on an external network (e.g., home network or campus network)
- Your router runs DDNS and port forwards to your node.js server. Put the pi and ESP32s on a site where you can access the DDNS configuration for your router. 
- Setup your node.js server (laptop) with static IP (assigns same subnet IP every time to MAC address of your laptop)
- Node.js server is on the local subnet and talks to the ESP32
- ESP32 is on the subnet of your router and talks to the node.js sever
- Setup ESP32 with static IP on subnet (as per MAC address). Static IP address assignment by MAC is configured in Devices tab of router.
- ***It will be very difficult to debug a system brought up all at once.*** You need to test the individual parts first
-- The skill assignments represent the individual parts -- make these work first
- Test your networking pieces on the local network first, then add the remote parts (it won't work remotely if it does not work locally)
- Build your node server on your laptop first; make sure it works, then port to pi
- Also, it is possible to host multiple http (web) servers on the pi
  - One url/port for camera
  - One inside node server


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


