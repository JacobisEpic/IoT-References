# E-Voting

Here we dabble with electronic voting which has important security
considerations on its own but also highlights important distributed
decision-making problems that affect collections of independent
computers.

We've decided that e-voting will be enabled by unique devices (fobs)
given to all registered voters. This is sort of like ID cards except
that we can control what data makes the devices unique and can
manipulate the interface to the voting 'machine.'  Voting will consist
of creating a secure near field communications link between two
fobs. Once the vote is passed to a fob, it is then propagated to a
single node that will tabulate the results and report out to a
server. The physical architecture is illustrated below.

<p align="center">
<img src="/docs/images/voting-arch.jpg" width="100%" />
</p>
<p align="center">
<i> Fob Voting Architecture</i>
</p>

Here's the twist: the voting 'machine' will be the set of all fobs in
your team (should be 6). In order to vote, the fobs will need to be
connected by IP networking.

## Rules in Play
We have the following rules in play for our voting process:

1. The code for each device should be identical with the exception 
of the device ID associated with each fob
2. Original votes can only be communicated by a secure IR channel from
one fob to another. 
3. Once the vote has been received, it should be communicated to the Poll Leader
4. The Poll Leader will send the results to a server (pi) which will log the vote to a database
5. Poll results will be accessible via the server via http 
6. The web server will be able to do a complete restart of the vote
7. The Poll Leader should be selected from your set of fobs
8. If the Poll Leader fails, a new one should be selected

<center><img src="/docs/images/e-vote-fsm.png" width="100%" /></center>
<center>E-Vote Dataflow</center>



## Description of the Fob
The voting fob works like this:
1. The design of the fob is the same as the transceiver in the IR TX/RX skill
2. A button on the fob is pressed to select the vote (Red, Green, Blue)
3. Another button initiates a short range near-field communications
  (NFC) message to transmit to another fob
4. The adjacent fob displays the vote by LED state (Red, Green, or Blue) as a diagnostic
5. The adjacent fob then communicates to the Poll Leader who tracks your vote and sends the vote to the server running a database
6. If the Poll leader fails, another one is selected and the process continues

<center><img src="/docs/images/ir-beacon.jpg" width="70%" /></center>
<center>IR TX/RX Transceiver </center>



## The Database and Web Server
1. The database logs each successful vote including time stamp and fob_ID
2. Queries to database shown in the web interface will reveal
    - List of candidates with their vote counts
    - List of individual votes by ID and time 
    - Remaining unsubmitted votes (optional)
3. A command from the web interface will reset the vote counts as a reset

## Assignment
1. Design and build your solution as described above 
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question:
- List 5 different ways that you can hack the system (including influencing the vote outcome or prevenging votes via denial of service)
- For each above, explain how you would mitigate these issues in your system.


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

6. Do this last, once the above works: Implement a failover method if
the Poll Leader is shut down. A new Poll Leader must be selected
within 45 sec.

7. Optional: message from Poll Leader confirming the vote received
back to the original voter (LED blink)

<p align="center">
<img src="/docs/images/order.png" width="100%" />
</p>
<p align="center">
<i>Recommended Development Sequence </i>
</p>

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

