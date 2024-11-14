# State Models	

State models are an excellent way to represent embedded system
scenarios. Familiar examples are an elevator, or a traffic light, or a
vending machine, but many other scenarios arise in computing that are
captured using states and transitions.

A few definitions
- States -- a place in the computation, usually a finite set
- Transitions -- the conditions that lead to moving from one state to
  another, usual inputs or events
- Models -- ways to capture the interaction between events and states. We will
consider state transitions matrices and FSMs

Wikipedia has good detail on finite state machines (FSMs) or just
state machines.  State tansision tables usually show a set of current
states as columns, and inputs (events) as rows. The table entries are
next states based on the inputs.

Wiki models a turnstyle

<p align="center">
<img src="/docs/images/turnstyle.png" width="80%">
</p>
<p align="center">
<i> FSM Model
(By Chetvorno - Own work, CC0, https://commons.wikimedia.org/w/index.php?curid=20269475)</i>
</p>

This can also be represented with the table

| Event/State | Locked | Unlocked |
|---|---|---|
|Push|Locked|Locked|
|Coin|Unlocked|Unlocked|

So there we are.

So here is a more abstract state machine: driving a car 
point-to-point.  Imagine that you start at Paul Revere Park,
N. Washington St. Boston and you are going to Minute Man National
Historical Park. Google will give you turn by turn instructions.

<p align="center">
<img src="/docs/images/waypoint.png" width="100%">
</p>
<p align="center">
<i> Directions Are a Set of Waypoints </i>
</p>

Getting from A to B requires many small line segments. Model the
route as (a) driving, (b) turing left, (c) turning right. 

## Assignment
1. Build a state table for this problem
2. Implement in C where transitions are caused by keyboard input (L, R)
3. Report

## Reference material
- [Design Pattern for FSMs in C](/docs/design-patterns/docs/dp-state-machine.md)
- [FSM on Wiki](https://en.wikipedia.org/wiki/Finite-state_machine)

