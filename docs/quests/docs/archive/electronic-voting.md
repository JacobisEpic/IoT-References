# E-Voting

Here we dabble with electronic voting which has important security
considerations on its own but also highlights important distributed
decision-making problems that affect collections of independent
computers.

Also, remember to vote. ***Election day is Nov. 3.***

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

Here's the twist: the voting 'machine' will be the set of all fobs in your team (approx. 9). In
order to vote, the fobs will need to be connected by IP networking.

We have the following rules in play for our voting process:

1. Original votes can only be communicated by a secure IR channel from
one fob to another. Once the vote is in the system, it can be
communicated to the Poll Leader using WiFi
2. The Poll Leader needs to be elected by the set of active fobs
3. The Poll Leader can render a winner after a sufficient number of reponses have been received (what number?)
4. If the Poll Leader fails or is out of network range, then a new Poll Leader must be elected
5. Poll results are logged at a server (pi) and accessible by a web browser
6. Votes from each fob are indicated by LED state (Red, Green, or Blue) as a diagnostic
7. The Poll Leader can reset the vote to start over

## Description

The voting fob works like this:
  - A button on the fob is pressed to select the vote
  - Another button initiates a short range near-field communications
  (NFC) message to transmit to another fob
  - The adjacent fob then communicates to the Poll Leader who tracks your vote and sends the vote to the pi running a database
  - When the Poll leader fails, another one is elected and the process continues
  - The database logs each successful vote including time stamp, and fob_ID
  - Queries to database will reveal
    - Vote counts and values
    - Remaining uncounted votes 
    - Time since first vote


<center><img src="/docs/images/vote-flow.png" width="80%" /></center>
<center>E-Vote Dataflow</center>

#### Additional Notes

- A ***vote*** is a successful exchange of data by a fob_ID to an adjacenent one
- Your "code" can be what your team defines. Consider a 4 digit number (PIN) or passphrase (text string)
- The design of the fob is the same as the transceiver in the IR TX/RX skill
- If you are short of ESP32s, you can build a fob with a switch to toggle the ID used (programmable ID)

<center><img src="/docs/images/ir-beacon.jpg" width="70%" /></center>
<center>IR TX/RX Transceiver </center>

## Investigative question



## Assignment
1. Design and build your solution to meet criteria
specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: 
    - List 5 different ways that you can hack the system (including influencing the vote outcome or prevenging votes via denial of service)
    - For each above, explain how you would mitigate these issues in your system.

## Stretch Objective
Implement to work engaging each team member's fobs across the open
internet. This will require port forwarding, DDNS, and tolerance to
delays and dropped packets if UDP is used.

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
