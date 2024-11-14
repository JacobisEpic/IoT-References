# Straba Social Media Hub

In this quest you will be creating portal for hosting data originating
from multiple Carmins. The main skills here relate to sourcing data
across a wireless network and making data available from any
browser.The concept is illustrated below. Here we collect data from
individual smart watches, aggregate them, and show leaders for
specific metrics (e.g., steps).

<p align="center">
<img src="/docs/images/straba-concept.jpg" width="80%">
</p>
<p align="center">
<i>Straba Social Media Hub Concept</i>
</p>

Each unit will be configured based on the Carmin quest except that now
we will send data via WiFi to a node server for aggregation and
reporting. You will need to build multiple Carmins for this quest. We
also incorporate a camera streamer to emulate the Peloton scenario of
personal video.

<p align="center">
<img src="/docs/images/straba-details.jpg" width="80%">
</p>
<p align="center">
<i>Straba Components</i>
</p>

In terms of networking, a key part of this exercise is to be able to
pass data across the open internet, through routers, in a
bidirectional way.

<p align="center">
<img src="/docs/images/straba-network.jpg" width="80%">
</p>
<p align="center">
<i>Straba Network </i>
</p>

 
## Solution Requirements

The key features of the Straba Hub are:
- Carmins connected via WiFi
- Collecting data from multiple Carmins to central server and presenting data as web portal
- Central server reports leader status back to each Carmin alpha display
- Central server runs on node.js, enables portal,  and is accessible on open Internet
- Webcam sourcing video from pi cam, embedded in a single client browser window


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions


## Tips
- The client browser should be on an external network (e.g., home network or campus network)
- Your router runs DDNS and port forwards to your node.js server. Put the RPi and ESP32s on a site where you can access the DDNS configuration for your router (a router will be provided)
- Setup your node.js server (laptop) with static IP (assigns same subnet IP every time to MAC address of your laptop). Your tomato router will do this for you
- Central Node.js server goes on the local subnet and talks to the ESP32s
- ESP32s are on the subnet of your router and talk to the node.js sever
- Setup ESP32s with static IPs on local LAN subnet (as per MAC address). Static IP address assignment by MAC is configured in Devices tab of router.
- ***It will be very difficult to debug a system brought up all at once.*** You need to test the individual parts first
- The skill assignments represent the individual parts -- make these work first
- Test your networking pieces on the local network first, then add the remote parts (it won't work remotely if it does not work locally)
- Build your node server on your laptop first; make sure it works, then port to the Pi
- Also, it is possible to host multiple http (web) servers on the pi
  - One URL/port for camera
  - One inside node server


## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Carmins connected via WiFi |  |  1     | 
| Data from each Carmin sent to central server and aggregated |  |  1     | 
| Portal reports live leader status and charts on web site |  |  1     | 
| Central server reports live leader status back to Carmin alpha displays |  |  1     | 
| Portal accessible from open internet |  |  1     | 
| Web cam operational in same browser window at client |  |  1     | 
| Node.js runs on pi |  |  1     | 
 


## Reference material
- [WiFi Station Example](https://github.com/espressif/esp-idf/tree/master/examples/wifi/getting_started/station)
- [UDP client](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sockets/udp_client)

