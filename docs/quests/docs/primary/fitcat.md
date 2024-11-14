# FitCat -- Activity Tracking for Cats

In this quest you will be creating portal for hosting data originating
from multiple Cat Trackers. The main skills here relate to sourcing
data across a wireless network and making data available from any
browser. The concept is illustrated below. Here we collect data from
individual Cat Trackers, aggregate them, and show leaders for specific
metrics (e.g., amount of active time). We also introduce sourcing a
signal from a remote location to trigger an event on a wireless
device.

<p align="center">
<img src="/docs/images/fitcat0.jpg" width="100%">
</p>
<p align="center">
<i>FitCat Activity Leaderboard Concept</i>
</p>

Each unit will be configured based on the Cat Tracker quest except that now
we will send data via WiFi to a node server for aggregation and
reporting. You will need to build multiple Cat Trackers for this quest. We
also incorporate a camera streamer to allow cat owners to look at the cats in the kennel.

In terms of networking, a key part of this exercise is to be able to
pass data across the open internet, through routers, in a
bidirectional way.

<p align="center">
<img src="/docs/images/fitcat1.jpg" width="80%">
</p>
<p align="center">
<i>FitCat Networking Components </i>
</p>

 
## Solution Requirements

The key features of the FitCat system are:
- Cat Trackers connected via WiFi
- Collecting data from multiple Cat Trackers to central server and presenting data as web portal
- Central server reports leader status back to each Cat Tracker alpha display and buzzer alerts cat to leader status
- Central server runs on node.js, enables portal,  and is accessible on open Internet
- Webcam sourcing video from pi cam into a window on the client machine 
- Leader criteria: Over the previous rolling 10 minutes, the cat with the most cumulative time-in-active state plus time-in-highly-active state is the leader among all connected cats
- All cats get buzzed on a leader change


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
| Cat Trackers connected via WiFi |  |  1     | 
| Data from each (5) Cat Tracker sent to central server and aggregated |  |  1     | 
| Portal reports live leader status for each activity state for each cat and charts them on web site |  |  1     | 
| Central server reports live leader status back to Cat Tracker alpha displays and buzzer |  |  1     | 
| Portal accessible from open internet |  |  1     | 
| Web cam operational at the same client |  |  1     | 
| Node.js runs on pi |  |  1     | 
 


## Reference material
- [WiFi Station Example](https://github.com/espressif/esp-idf/tree/master/examples/wifi/getting_started/station)
- [UDP client](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sockets/udp_client)

