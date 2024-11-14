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
state machines.  State transition tables usually show a set of current
states as columns, and inputs (events) as rows. The table entries are
next states based on the inputs.

Here is an example from Wiki that models a turnstile that takes a coin to allow
a person to pass.

<p align="center">
<img src="/docs/images/turn.jpeg" width="30%">
</p>
<p align="center">
<i> A Turnstile </i>
</p>

And here is the Wiki FSM of the behiavior.

<p align="center">
<img src="/docs/images/turnstyle.png" width="60%">
</p>
<p align="center">
<center> FSM Model
(By [Chetvorno - Own work, CC0](https://commons.wikimedia.org/w/index.php?curid=20269475)</i>
</p>

This can also be represented with the table

| Event/State | Locked | Unlocked |
|---|---|---|
|Push|Locked|Locked|
|Coin|Unlocked|Unlocked|


## Assignment
1. Build a FSM model for the the behavior of a self-service gas pump (swipe a card, pump the gas, etc.)
2. Build a corresponding state table
3. Pick one of the appoaches to coding a state machine shown in the design pattern, and provide c code
matching your gas pump state machine
3. Report your results (graphics or text)

## Reference material
- [Design Pattern for FSMs in C](/docs/design-patterns/docs/dp-state-machine.md)
- [FSM on Wiki](https://en.wikipedia.org/wiki/Finite-state_machine)

<!---
[whack-a-mole game](https://www.crazygames.com/game/whack-a-mole)
--->