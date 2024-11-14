# Secure Election with NFC

As this is a presential election year, we want to offer a technical
solution for ensuring a valid and secure balloting approach using a
convenient wireless approach. To this end, you will be creating a
wireless voting fob and using near field communications

The use of NFC (near-field communications) is for improving security
at the point of exchanging information from a user device (the fob) to
the infrastructure (the voting box). NFC is commonly used for credit-card
transactions using RFID or similar short range RF. We will use two NFC
methods: IR comms and QR codes.

<p align="center">
<img src="/docs/images/vote2.jpg" width="100%">
</p>
<p align="center">
<i>Secure Voting NFC System</i>
</p>

## Architecture and Data Flow

The more detailed view of the architecture is shown below. We will use
an NFC device comprised of IR LEDs and IR receivers and hosted on an
ESP. An RPi with pi camera is used to decode a dynamically generated QR code with the
meter ID to solve the 'provisioning' problem.

<p align="center">
<center><img src="/docs/images/vote1.jpg" width="100%">
</p>
<p align="center">
<i>Key Fob System Architecture and Data Flow</i>
</p>

The flow is indicated by the numbers in the illustration as follows:
1. A button press sends {fob ID} to the voting box using IR TX/RX
2. The box generates a QR code* with {meter ID, fob ID}
3. The fob reads the QR code for {fob ID, box ID}
4. The fob sends {box ID, fob ID} to the Auth server
5. Auth server validates {fob ID, box ID} and logs status, returns {box key, status}
6. The {box key, status} is sent to fob and to box
7. Based on box status, the vote is counted or not (LEDs indicate status)
8. Web client access shows status of each voter by supporting queries
on the database

There are many opportunities here to make this sequence
more robust and more secure.

*The QR codes can be pre-generated and hardcoded into the firmware. 


## Solution Requirements
1. The design of the fob is the same as the transceiver in the IR TX/RX skill (except one is a transmitter and the other is a receiver)
2. The voter box device should include R, G, B LEDs as indicators
4. The Auth Server should log all transactions including FIB, MID, timestamp
5. The database can be accessed by fixed queries (e.g., show last 10 entries of transaction data)
6. A state machine must be provided describing the system behavior for casting a ballot

<p align="center">
<img src="/docs/images/ir-beacon.jpg" width="40%">
</p>
<p align="center">
<i>IR TX/RX Transceiver as Basis for Fob Device </i>
</p>

## Assignment
1. Design and build your solution as described above 
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: How can our secure voting be hacked? (a) Describe two scenarios and (b) explain how you can improve
our system to mitigate these hacks. 


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
| Fob sends (IR TX/RX) FID to voting box                |        | 1   | 
| Box ESP displays QR code with BID,FID                |        | 1   | 
| Fob Pi reads QR code on box and sends (WiFi) to Auth Server with BID,FID                |        | 1   | 
| DB logs BID,FID,timestamp and validates box status (voted/not voted); sends (WiFi) BID, status to fob and box                 |        | 1   | 
| Box evaluates status and sets LEDs to indicate vote successful              |        | 1   | 
| Web client accesses Auth Server to show logged data and voter status                  |        | 1   | 
| Auth Server implemented in TingoDB and on separate Pi                 |        | 1   | 
| Investigative question response                                                           |        | 1   | 