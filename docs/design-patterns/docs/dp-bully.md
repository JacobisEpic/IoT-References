# Design Pattern for the Bully Algorithm

## Basics

The Bully Algorithm, described
[here](https://en.wikipedia.org/wiki/Bully_algorithm), facilitates
electing a coordinator in a distributed system. The basic approach is
for a device (process) in a distributed system to initiate an election
by broadcasting an election request 'e' to all devices. They each
respond with an answer and their ID as 'a(ID)'. The results are
received by the all devices (since the data are broadcast) and every
device is able to identify the max value. The device with the maximum
value then declares itself as the election victor with a broadcast
message 'v(max-val)'.

<p align="center">
<img src="/docs/images/bully.jpg" width="70%">
</p>
<p align="center">
<i> Election Request Propagation in Bully Algorithm</i>
</p>


In this DP we will explore how to adapt the Bully Algorithm to the
nuances of our hardware.

First of all, we recognize that we do not have a "true" broadcast. In
our system we will send each message in a peer-to-peer mode, on a
local subnet (i.e., directly from one IP address to another. This
means other devices cannot "listen-in" on the same data stream. To
implement "broadcast" we need to send a message to each device in the
system, one at a time.

Second, we don't really know how what devices are on our system
without some hints (i.e., we do not have a "discovery" process). So we
will assume that we know each of the devices in our universe (say, n
devices). For each n, we have a known ID and IP:port address.

In this way we can send messages to every device by cycling through
each of the IDs listed in our universe. However, we will expect that
sometimes one or more devices may be currently turned off or out of
range. This is an anomaly that we will need to address in the
algorithm.

There are other things that we need to anticipate:
- What happens when the system starts? Not every device will be turned on at the same time
- What happens when an isolated device that thinks it is a coordinator joins the network already with a coordinator?
- What happens if a device fails in the middle of an election?
- Under what conditions does a device initiate a new election?
- How does a coordinator ensure that other devices know it is still active?

In the following we provide some approaches to these scenarios.

### Cold Start Boot
There are multiple options for the cold start boot:

1. On cold start all devices begin as coordinators
- Each device sends coordinator message to all other devices with own ID
- All receiving devices decide if they have the lowest ID
- Lowest ID remains coordinator; all others are not
2. On cold start all devices begin as non-coordinators
- Devices timeout and then each send an election request
- Each responds with ID; all devices pick lowest ID
- Lowest ID responds as coordinator

### Message Content
What information should be in the message?
- Message type (e, a, v, k), ID
- e -- election
- a -- answer()
- v -- victor()
- k -- keep-alive
- ID -- ID of sender

### Timeouts
Timeouts can mitigate problems with lost messages or devices
disconnecting from the network, Implement timeouts as timers
that trigger interrupts as events that cause state transitions. 

Possible timeouts implemented on each device:
- Coordinator timeout – the Coordinator failed to send me a keep-alive message (k)
- Election timeout – I have waited long enough to receive election messages so I will:
  - (If I have the lowest ID) Declare victory and send a victory message and keep-alive messages, OR 
  - (If I do not have lowest ID) Begin a new coordinator timeout period because someone else must be claiming victory

### Modeling with States and Events
Model per device
- Timeouts are events (trigger transitions to new state)
- Values of sent messages are events (trigger transitions to new state)
- States are going to be something like (you will decide)
  - Leader
  - Election, but not a leader
  - Not a leader

The overall system can be viewed as having a state too. But you are
focused on the model of a single device -- all devices should have the same code but different IDs

### Summary Details for Implementation
Message format (type, ID)
- a – answer
- e – election
- v – victory
- k – keep-alive
- ID – ID of sender

Format as:

| Start | type | ID | checksum |
|---|---|---|---|
|0x1B|e|01|xx|

See traffic light code example for formatting and use of checksum.

Addressing
| ID | IP:port |
|---|---|
|01|192.168.1.10:3000|
|02|192.168.1.11: 3001|
|03|192.168.1.12:3002|
|03|192.168.1.13:3003|

Timers
- Coordinator timer
- Election timer
- Keep-alive timer (Coordinator only)



## Reading and Reference Material
- [Bully Algorithm](https://en.wikipedia.org/wiki/Bully_algorithm)