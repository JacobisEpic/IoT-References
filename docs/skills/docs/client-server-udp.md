# Client and Server UDP on ESP32 and Node 

In this skill you will set up a link for a client (sends data) and a
server (listens for data) application in which the ESP32 is the
client, and then later, a server.

This is the key to bidirectional communications and remote control
over a wireless network (or any network). In this skill you will set
up links for each direction between a client and a server application.

In this exercise you will demonstrate basic communication between the
ESP32 and some other device on the network. There are lots of
scenarios for this A--B communication where 'A' and 'B' are devices
such as ESP32s or laptops but here we keep it simple. Examples include
using Bluetooth or WiFi. Variations include:

1. A -- Router -- B (WiFi). This is normal hierarchical WiFi with a router as a hub
2.  A -- B (WiFi). This is called DCF in WiFi; an 'ad hoc' point-to-point connection
3.  A -- dongle -- B (BLE). This uses a BLE dongle as the PAN coordinator and bridge
4.  A -- B (BLE). One of A or B needs to be the PAN coordinator

<p align="center">
<img src="/docs/images/esp-wifi.png" width="80%">
</p>
<p align="center">
<i>WiFi or BLE Network Options</i>
</p>

We're going to consider the base case in which each ESP32 connects via
WiFi to the router (Case 1) using UDP. Each connecting ESP32 must be set
up to connect to a WiFi router.  This assignment assumes that each
device has been enabled for WiFi connection.


## Setup

Configure endpoint A as a laptop and endpoint B as an ESP32 as follows
(IP addresses do not have to be exactly as shown):
- A: IP address 192.168.1.10
- B: IP address 192.168.1.11
- Use ports such as 3333, 4444, 8080 as required

## Assignment (team skill)
1. Read the [Design Pattern for UDP
Sockets](/docs/design-patterns/dp-sockets.md). This DP shows
how to set up a node.js UDP server (listens for data) on a laptop and
a UDP client (sends data) on the ESP32.

2. Node app as server at the laptop and ESP32 as client
     - Bring up a UDP server in the node app 
     - Bring up a UDP client at the ESP32 including WiFi 
     - Demonstrate by the ESP32 sending a request for blink time to the server; the server responds with a new blink time; and the ESP32
     changes the on-board LED blink time

2. Now bring up the corresponding client at the laptop and server at
the ESP.
     - Bring up a UDP client in the node app 
     - Bring up a UDP server at the ESP32 including WiFi
     - Demonstrate by the node app sending a message to the ESP32 to turn on a GPIO LED; the ESP32 responds to the node server acknowledging the
     change
     
3. Write up, report, and show evidence that this all works

## Reference Code
- [ESP32: WiFi Driver](https://github.com/espressif/esp-idf/tree/master/examples/wifi/getting_started/station).
This is the WiFi skill.
- [ESP32 UDP Client](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sockets/udp_client)
- [Design Pattern for UDP Sockets](/docs/design-patterns/docs/dp-sockets.md)
- [ESP32 UDP Server](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sockets/udp_server)

