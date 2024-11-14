# E-Voting

Here we dabble with electronic voting which has important security
considerations on its own but also highlights important distributed
decision-making problems that affect collections of independent
computers.

<p align="center">
<img src="/docs/images/dist-syst1.jpg" width="80%" />
</p>
<p align="center">
<i> Secure Voting Concept</i>
</p>

In our model, a single device will be chosen to be coordinator in a distributed
system. The coordinator will authenticate participants in voting 
(see above). Participation in the vote will be restricted to devices
that have authenticated by near field communications (NFC). And in our
model, the devices are fobs that are given to individual people
("voters").

To particpate in the voting, fobs must connect via NFC to a member of
the wireless distributed system. This will be done with a secure IR
link.  The member then passes the ID and vote to the elected
Coordinator.  The Coordinator then sends the ID and vote to the
database server for logging, and provides a confirmation to the
oringal voter.


<p align="center">
<img src="/docs/images/newbie.jpg" width="80%" />
</p>
<p align="center">
<i> Near Field Communication for Connecting Voter</i>
</p>

The steps and data flow for this process are shown below. 

<p align="center">
<img src="/docs/images/system-leader.jpg" width="80%" />
</p>
<p align="center">
<i> Data Flow for Voting</i>
</p>

So in essence there are two levels of "voting" going on here. One is
to "elect" a coordinator of the distributed system and the other is to
pass a vote from a voter, through the NFC, to the coordinator and then
the server.

A critical step in this system is to ensure that the coordinator is
alive and connected. This is the meaty part of the quest that comes
from the "Leader (Coordinator) Election" skill.  We need to deal with
what happens when the coordinator drops out and a new one needs to be
selected from the remaining members.

## Rules in Play
We have the following rules in play for our voting system:

1. The firmware should be identical for each fob device with the exception 
of the device ID which must be unique
2. Fobs, when booting up, should connect to the distributed system of devices via WiFi.
3. To vote, a human must connect the fob to another device via NFC (IR) to pass an ID and vote to
the system. 
4. The IR receiving device will send the ID and vote to the current Coordinator
5. The Coordinator will send the ID and vote to the database server and a confirmation back to the original voting fob
6. Poll results will be accessible via the pi server via http 
7. The web server will be able to initiate a reset of the database
8. The coordinators fails, an election will lead to a repalcement coordinator and the system will still function


## Fob Hardware
We will use the same fob design as the transceiver in the IR TX/RX
skill with some functional changes:

1. A button on the fob initiates a short range near-field communications
  (NFC) message to transmit to another fob
3. The adjacent fob should display the operating state using the LEDs (Red, Green, or Blue) as a diagnostic
5. The adjacent fob then communicates to the Coordinator who  sends the Fob ID and vote to the server running a database
6. If the Coordinator fails, another one is selected via leader election and the process continues
7. The orignal fob gets confirmation and displays status via LED
8. Votes can be conveyed as Red, Blue, Green)

<p align="center">
<img src="/docs/images/ir-beacon.jpg" width="35%" />
</p>
<p align="center">
IR TX/RX Transceiver
</p>


## The Database and Web Server
1. The database logs each successful vote including time stamp and fob_ID
2. Queries to database shown in the web interface will reveal
    - List of fobs with their vote and when occurred
    - Current vote totals (Red, Blue, Green)
3. A command from the web interface will reset the database to empty

## Assignment
1. Design and build your solution as described above 
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative questions:
- List three different ways that you can hack the system 
- For each above, explain how you would mitigate these issues under your design


## How to Approach this Quest
We recommend that you follow this sequence

1. Complete the IR-TX/RX Skill: build fobs and bring up TX/RX code to
demonstrate it works: Adapt code to transmit vote (R, B, G) using IR

2. Set up UDP message passing on your local wireless network: build a
method to exchange payloads to one or more destinations (e.g.,
point-to-point or point-multipoint). Make sure it works from fob to coordinator 
and coordinator to node.js

3. Complete the Database Skill: set up tingodb or equivalent on your
server for the vote data and be able to receive and save data from the
coordinator to the node.js and to the DB.

4. Interconnect your node.js server to the DB and host the queries for
the vote data on a web page.

5. Integrate these steps into as single application that is loaded onto all of the fobs.

6. Combine the Coordinator election process and demonstrate what happens when the Coordinator
fails. A new Coordinator should be elected to replace the failed one. 

## Rubric


| Objective criteria (0/1, 1=met)                                                           | Rating | Max | 
| ----------------------------------------------------------------------------------------- | ------ | --- | 
| Vote and Fob ID passed via NFC to connected device              |        | 1   | 
| Connected device passes {FID, Vote} to Coordinator                 |        | 1   | 
| Coordinator sends {FID, payload} to server |        | 1   | 
| Coordinator sends confirmation of vote to orignal fob  |        | 1   | 
| LEDs indicate state of each unit: Coordinator or non-coordinator              |        | 1   | 
| Database server logs exchange (FID, vote, timestamp |        | 1   | 
| Web client accesses server to show tabluated data and vote totals                  |        | 1   | 
| Database implemented on pi                  |        | 1   | 
| Successful coordinator election and failover |        | 1   | 
| Investigative question response     |        | 1   | |  |        | 1   | 
