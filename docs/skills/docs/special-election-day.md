# Special Election Day Election Challenge

Being that it is a special election day in the US (first Tuesday in
November), we will do an election problem.  We will cover two skills:

1. Leader Election
2. State Models


## Leader Election

Leader election in computer systems relates to identifying one process
or entity to take charge of coordinating activities across a set of
processes or devices.  A great example is illustrated in car
platooning.

<p align="center">
<img src="/docs/images/platoon.jpg" width="70%">
</p>
<p align="center">
<i>Car Platooning</i>
</p>

In this example, one vehicle (the leader) establishes direction and
speed for a set of trailing vehicles and they all lock-in. Platooning
provides various benefits of energy savings, reducing congestion, and
self-driving.   The leader is essential for controlling the other entities.

Leaders are elected using different algorithms (see [Leader Election](/docs/skills/docs/leader-election.md) for more
detail). For this exercise we will select a leader based on lowest
device ID in a connected network, and the other devices will be
followers.

Key properties of our system for leader election are:
- Elect exactly one leader
- Everyone becomes aware of the leader
- The election does not last forever
- If the leader fails, a new leader election is initiated

This brings us to the other part: State Models

## State Models

Also called out in a separate skill (see [State
Models](/docs/skills/docs/state-models.md)), state models are useful
for problems that model well as a recurring and finite set of "states"
and conditions that lead to changing from one state to
another. Examples include traffic lights, elevators, smart appliances,
user interfaces, etc.  The models are probably most useful to
conceptualize behavior of some system; but it is possible to translate
such a conceptualization into C code, which we will do.

A few definitions
- States -- a place in the computation, usually a finite set
- Transitions -- the conditions that lead to moving from one state to
  another, usual inputs or events
- Models -- ways to capture the interaction between events and states. We will
consider state transitions matrices and FSMs

So that's it for now. There is more detail in the skill problems for
state models and for leader election.

## Election Day Special Challenge

Your Assignment (in class only) is to develop the state model for the
election transceiver (fob) so that the system achieves the election
behavior described below. We're giving you most of the code for the
communication and integration. It's also demonstrating some of the
advanced features of FreeRTOS, namely tasking, mutex, queues,
semaphores, but that's because Emily was flexing her coding
muscles. It could be done in an more modest way too.


1. Build up the ***Wireless Election Fob***, as shown below (one per student)
2. As a team, copy over the code from the [ir-election](https://github.com/BU-EC444/04-Code-Examples/tree/master/ir-election) folder on the class repo.
This has all of the code to implement data exchange between your fob and other fobs in the system.
3. You will need to modify the code as follows:
   - Add a state model for the behavior described below (implemented in C)
   - Install the code in each of your ESP32s each with an unique ID corresponding to your (not team) kit number
4.***Must be complete by 2:45PM (no exceptions)***
5. Voting activity begins at 2:50PM

## Wireless Election Fob
Build this out -- one per person

<p align="center">
<img src="/docs/images/leader-led.png" width="60%">
</p>
<p align="center">
<i>Wireless Election Fob</i>
</p>

<p align="center">
<img src="/docs/images/ir-election-schem.png" width="100%">
</p>
<p align="center">
<i>Wiring -- Schematic</i>
</p>

<p align="center">
<img src="/docs/images/ir-election_bb.png" width="100%">
</p>
<p align="center">
<i>Wiring -- Breadboard</i>
</p>



## Leader Election Algorithm
- Convert to a state model
- Implement in C as a team

This "spec" is intentionally loose so that you can work to make it stateful.

***Specification***
- Each node has a unique ID in the range of 0--50 corresponding to your kit number
- Lower IDs have priority
- Each node is initially an unassigned (U) state with MinID = ID; they may become leaders (L) or followers (F)
- Nodes are asynchronous -- things happen without synchronization
- Leaders show a blue LED, followers show a green LED, and unassigned show red LED
- Nodes wander around and connect with other nodes ("activity")
- When two nodes meet, they exchange their status (U,L,F), their IDs, and their MinID value
- If one of the nodes is unassigned, then MinID for both nodes is set to  the ID of the lowest of the pair,
 and the nodes assume their role depending on their IDs (one becomes leader,
the other follower)
- If the nodes are (leader, leader), (follower, leader), or (follower, follower), the nodes assume a new state based
on the values of the exchanged MinID (assigned the lowest of the two) and then set appropriate status (one or both may become followers)
- By repetitive interactions, the MinID will propagate through the system and within a connected set, a single leader should emerge
- Pressing a button on the ESP32 will cause the node to enter the unassigned state and reset MinID = ID
- Although you each should have a unique ID, define a rule for the situation where two nodes have the same ID.

## Reference material
- [Design Pattern for State Models in C](/docs/guides/design-patterns/dp-state-machine.md)
- [FSM on Wiki](https://en.wikipedia.org/wiki/Finite-state_machine)
- [Leader Election](https://en.wikipedia.org/wiki/Leader_election)


<p align="center">
<img src="/docs/images/voting-beacon.jpg" width="80%">
</p>
<p align="center">
<i>Wired Voting Fob with IR TX/RX</i>
</p>

<p align="center">
<img src="/docs/images/voting-ring.jpg" width="80%">
</p>
<p align="center">
<i>Voting Group </i>
</p>

<p align="center">
<img src="/docs/images/voting-exch.jpg" width="80%">
<p align="center">
<i>Voting Exchange </i>
</p>
