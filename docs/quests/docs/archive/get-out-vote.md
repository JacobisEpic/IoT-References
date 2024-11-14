# NFC Scooter Key Fob

In this quest you will be creating a secure key fob that is used to
unlock an e-scooter. The techique used is intended to improve security
by requiring proximity to the selected scooter and the use of near
field communications (NFC) which are more difficult to intercept as an
"eavesdropper". The figure below illusrates the concept including the
possibility for a malicious user to be part of the system.

<p align="center">
<img src="/docs/images/key-fob-overall.png" width="100%">
</p>
<p align="center">
<i>NFC Key Fob System</i>
</p>

## Architecture and Data Flow

The more detailed view of the architecture is shown below. We will use
an NFC device comprised of IR LEDs and IR receivers and hosted on an
ESP. A RPi with pi camera is used to decode a local QR code with the
scooter ID (SID) to solve the 'provisioning' problem. The flow is
initiated by a button press on the fob that communicates to the
scooter (and RPi) to start the process (think state machine here).
Then the scooter then expects to receive a key from the Auth
server. The RPi is triggered to decode the SID from the QR code and
then send this along with its fob ID (FIB) to the Auth Server. The
athentication server validates the FIB and SID pair and then creates a
random key that is sent back to the fob and to the scooter via
separate messages. Upon receiving the key, the fob indicates, via LED,
that it is ready to communicate the key to the scooter. On button
press the FIB and key are sent to the scooter which compares the keys
sent via different paths. If they match, the scooter indicates success
via LED.

<p align="center">
<center><img src="/docs/images/key-fob-arch.png" width="100%">
</p>
<p align="center">
<i>Key Fob System Architecture and Data Flow</i>
</p>

# Solution Requirements
1. The design of the fob is the same as the transceiver in the IR TX/RX skill (except one is a transmitter and the other is a receiver)
2. The code for each ESP32 device should be identical (except that one receives and the other transmits) and be able to accept configuration data such as
device ID, device type (scooter or fob) and IP address. 
3. The fob/scooter device should include R, G, B LEDs as indicators
4. The Auth Server should log all transactions including FIB, SID, timestamp
5. The database can be accessed by fixed queries (e.g., show last 10 entries of unlocking transaction data)
6. A state machine must be provided describing the fob/scooter device behavior

<p align="center">
<img src="/docs/images/ir-beacon.jpg" width="80%">
</p>
<p align="center">
<i>IR TX/RX Transceiver as Basis for FOB/Scooter Device </i>
</p>

## Assignment
1. Design and build your solution as described above 
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: how would you hack this system? Describe two ways, and how you would change the solution to combat the hack.


## How to Approach this Quest
We ***strongly*** recommend that you follow this sequence

1. Complete the IR-TX/RX Skill: build fobs and bring up TX/RX code to
demonstrate it works: Adapt code to transmit the required data payload using IR.

2. Set up UDP message passing on your local wireless network: build a
method to exchange data payloads to one or more destinations (e.g.,
point-to-point). Make sure it works between entities in the data flow architecture.

3. Complete the Database Skill: set up a database on your
server for the logged data and be able to receive and save data from a client.

4. Interconnect your node.js server to the DB and host the queries for
the unlocking transaction data on a web page.

5. Integrate the PI camera, PI node server and the fobs into a single connnected
system.


## Rubric


| Objective criteria (0/1, 1=met)                                                           | Rating | Max | 
| ----------------------------------------------------------------------------------------- | ------ | --- | 
| Fob Pi reads QR code on scooter and sends (WiFi) to Auth Server with SID,FID                |        | 1   | 
| DB logs SID,FID,timestamp and sends (WiFi) key to fob and scooter                 |        | 1   | 
| Fob sends (IR TX/RX) FID,key to scooter                |        | 1   | 
| Scooter compares keys and indicates unlock or fail with LEDs              |        | 1   | 
| Web client accesses Auth Server to show logged data                  |        | 1   | 
| Auth Server implemented on separate Pi                 |        | 1   | 
| Investigative question response                                                           |        | 1   | 