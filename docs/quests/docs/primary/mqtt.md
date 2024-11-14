# MQTT

Here you will adopt
the MQTT model of publish and subscribe, with the ESP32s as publishing
data to a Message Broker (MB) and a client accessing the MB to render
data display and visualization.

<p align="center">
<img src="/docs/images/mb1.jpg" width="60%">
</p>
<p align="center">
<i>Message Broker Concept</i>
</p>

A key concept here is to buffer the capabilities of the end devices
(e.g., the ESP32s) which often must run on batteries with very low
power. The MQTT concept has these devices powering up at infrequent
times to sense then transmit data to an MB that is always on. Then the
always-on MB can serve data to subscribers on-demand.  When you look
at the MQTT code for the ESP32 you will notice multiple versions (ssl,
ws, wss, tdp etc.). These all work but rely on different selection of
a transport protocol. We recommend using the latest MQTT 5 for which
there tcp is used as the transport layer.


<p align="center">
<img src="/docs/images/mb2.jpg" width="60%">
</p>
<p align="center">
<i>Message Broker Details</i>
</p>

## Our implementation of the MQTT-based system

The ESP32s are supported by an MQTT API supporting the protocol. See
the distribution for details and example code. In the basic case we
set the ESPs to publish on a topic with a value (e.g., wireless
thermostats).

For a message broker, we will use one provided by mosquitto.org that
will run on the Pi. Finally, a client can be adopted or created that
will allow display on a laptop running remotely. We recommend creating
a node.js app that provides MQTT functionality (via imported module)
which passes data to a connecting browser using HTML and sockets, as
we have done previously. The new part here is that the node.js app
will pull data from the message broker rather than receiving data
directly from the ESP32 devices. This is also similar to pulling data
from a database.

We're providing some ideas for an application to construct for
this quest. You can consider some other app with approval:
- Re-implement the secure parking meter using MQTT where the client
displays status of meters and a map of available and occupied spaces
- Use sensors for seat occupancy in a coffee shop. The client shows a
map of available and occupied seats.
- Use ESP32s as voting fobs in an election of 8 candidates for 3
elected positions. The system must be secure, allow only one vote,
and show real-time update of vote counts. 

## Solution Requirements
1. Must use at least 3 ESP32s each running MQTT protocol
2. Message Broker on Pi
3. Client visualizes collected live data for set of ESP32 devices using tables and graphic (map, or chart)
4. Client can be on external network
5. Client can change the status of an LED or display on each ESP32 (e.g., an LED indicating a vote was made)

## Assignment
1. Design and build your solution as described above 
2. Demonstrate your work
3. Reporting as per quest reporting instructions


## Rubric


| Objective criteria (0/1, 1=met)                                                           | Rating | Max | 
| ----------------------------------------------------------------------------------------- | ------ | --- | 
| Using at least 3 ESP32s running MQTT protocol    |   | 1 | 
| Using MQTT Message Broker on Pi    |   | 1 | 
| Multiple Clients can subscribe to Message Broker    |   | 1 | 
| Client displays tabluated values from each ESP32     |   | 1 | 
| Client displays live visualization of device values as graphic (map, chart, etc.)    |   | 1 | 
| Client runs on external network    |   | 1 | 
| Client is able to change status of LED on each ESP32     |   | 1 | 

## Reference Material

-[ESP MQTT5 Example Code of data exchange with node](https://github.com/BU-EC444/04-Code-Examples/tree/main/mqtt5-exchange)
- [ESP MQTT API Guide](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/protocols/mqtt.html)
- [ESP32 MQTT5](https://github.com/espressif/esp-idf/tree/03414a15508036c8fc0f51642aed7a264e9527df/examples/protocols/mqtt5)
- [Message Broker for Pi](https://mosquitto.org)
- [Install MQTT on Pi OS](https://cedalo.com/blog/mqtt-broker-raspberry-pi-installation-guide/)

- [MQTT and Node.js NPM](https://www.npmjs.com/package/mqtt#example)
- [MQTT and Node.js](https://www.emqx.com/en/blog/how-to-use-mqtt-in-nodejs)
- [Example connecting to chartsjs](https://stackoverflow.com/questions/50018543/add-mqtt-topics-and-data-to-chartjs)
