# E-Voting

Here we dabble with electronic voting which has important security
considerations on its own but also highlights important distributed
decision-making problems that affect collections of independent
computers.

We've decided that e-voting will be enabled by devices (fobs) given to
each registered voter. Fobs are issued to voters after producing their
credentials (proof of registration, address).

<p align="center">
<img src="/docs/images/vote1.jpg" width="80%" />
</p>
<p align="center">
<i> Secure Voting Concept</i>
</p>

<!-- A human triggers (on a laptop) the generation of a time-limited ID
which is rendered as a QR code on the screen that is scanned by the
fob. Now the fob is ready to participate in voting. -->

Voting consists of creating a secure near field communications link
between two fobs in the system. Once a vote is passed to a fob, it is
then propagated to a single node that will tabulate the results and
report out the results. The physical architecture is illustrated
below.



<p align="center">
<img src="/docs/images/vote2.jpg" width="80%" />
</p>
<p align="center">
<i> System Components for Secure Voting</i>
</p>

Here's the twist: the voting 'machine' will be the aggregate set of
connected fobs. This distributed system has some nice robustness
properties such as failover if the leader quits.  In order to vote,
the fobs will need to be connected by IP networking.

## Rules in Play
We have the following rules in play for our voting process:

1. The firmware should be identical for each fob device with the exception 
of the device ID which must be unique
2. Fobs can participate in the distributed system after booting up, but must be associated with a voter ID before they can vote
3. A vote is only valid if it is passed to another fob using the NFC link 
4. Once a vote has been received by a fob it should be communicated to the Poll Leader
5. The Poll Leader will send the results to a server (pi) which will log the vote to a database
6. Poll results will be accessible via the pi server via http 
7. The web server will be able to do a complete restart of the vote
8. The Poll Leader should be selected from your set of fobs using leader election
9. If the Poll Leader fails, a new one should be selected

<p align="center">
<img src="/docs/images/vote3.jpg" width="75%" />
</p>

<p align="center">
Detail of System Components 
</p>



The data data flow is shown below. Note that there will be a separate
process for ensuring that the set of fobs has selected which fob will
be the Poll Leader.

<p align="center">
<img src="/docs/images/vote4.jpg" width="75%" />
</p>

<p align="center">
Data Flow for Voting
</p>



## Fob Hardware
We will use the same fob design as the transceiver in the IR TX/RX
skill with some functional changes:

1. A button on the fob is pressed to select the vote (Red, Green, Blue)
2. Another button initiates a short range near-field communications
  (NFC) message to transmit to another fob
3. The adjacent fob should display the vote by LED state (Red, Green, or Blue) as a diagnostic
5. The adjacent fob then communicates to the Poll Leader who tracks your vote and sends the vote to the server running a database
6. If the Poll leader fails, another one is selected via leader election and the process continues
7. You will need to decide how to authenticate the fob (associate a
voter with the fob ID) and how to limit multiple or fraudulent votes
from entering the system (this is unspecified and left to you to decide)

<p align="center">
<img src="/docs/images/ir-beacon.jpg" width="35%" />
</p>
<p align="center">
IR TX/RX Transceiver
</p>


## The Database and Web Server
1. The database logs each successful vote including time stamp and fob_ID (and possibly voter_ID)
2. Queries to database shown in the web interface will reveal
    - List of candidates (R, G, B) with their vote counts
    - List of individual votes by ID and time (and possibly voter_ID) 
    - Remaining unsubmitted votes (optional)
3. A command from the web interface will reset the vote counts as a reset

## Assignment
1. Design and build your solution as described above 
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative questions:
- Explain how you authenticate a voter when they receive a fob, and how you ensure the vote is singular
- List three different ways that you can hack the system 
- For each above, explain how you would mitigate these issues under your design


## How to Approach this Quest
We ***strongly*** recommend that you follow this sequence

1. Complete the IR-TX/RX Skill: build fobs and bring up TX/RX code to
demonstrate it works: Adapt code to transmit vote (R, B, G) using IR

2. Set up UDP message passing on your local wireless network: build a
method to exchange vote payloads to one or more destinations (e.g.,
point-to-point or point-multipoint). Make sure it works from fob to leader 
and leader to node.js

3. Complete the Database Skill: set up tingodb or equivalent on your
server for the vote data and be able to receive and save data from the
leader to the node.js and to the DB.

4. Interconnect your node.js server to the DB and host the queries for
the vote data on a web page.

5. Integrate these steps into as single application that is loaded onto all of the fobs.

6. Do this last, once the above works: Implement leader election if
the Poll Leader is shut down. A new Poll Leader must be selected
within 45 sec.

7. Optional: message from Poll Leader confirming the vote received
back to the original voter (LED blink)

## Rubric


| Objective criteria (0/1, 1=met)                                                           | Rating | Max | 
| ----------------------------------------------------------------------------------------- | ------ | --- | 
| Authentication of VID with FID                |        | 1   | 
| Fob sends (IR TX/RX) {FID, vote} to adjacent fob                |        | 1   | 
| Poll leader sends {FID, vote} to server |        | 1   | 
| Pi server logs vote, FID, and VID |        | 1   | 
| Web client accesses Server to show tabluated data and voter status                  |        | 1   | 
| Auth Server implemented in database and on separate Pi                 |        | 1   | 
| Investigative question response                                                           |        | 1   | |  |        | 1   | 
| Leader election and failover |        | 1   | 
| Box evaluates status and sets LEDs to indicate vote successful              |        | 1   | 
