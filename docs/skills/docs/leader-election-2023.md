# Leader Election

***This skill requires completing the IR TX/RX skill*** and having two
   units available. It also assumes that you have established how to
   communicate messages using UDP between any two ESP32s on a WiFi
   network.

In many distributed systems problems we require a single entity to
provide some control or synchronization function. In this skill you
will implement a leader election algorithm.

There are many variants, but the basic problems are to idenfity how to
elect one and only one leader, have every everyone accept the elected
leader, and to elect a new one if the old one disappears (falls off
the network).

These properites of leader election are summarized as:
- Elect exactly one leader
- Everyone becomes aware of the leader
- The election does not last forever
- If the leader fails, a new leader election is initiated


<p align="center">
<img src="/docs/images/leader-led.png" width="50%">
</p>
<p align="center">
<i>Base Unit for Leader Election</i>
</p>

There are many ways to realize the above. But we'll start with a base
defined by the Bully Algorithm. In order to make this work we need to
define some standard messages and a fully connected network
(ability to send and receive messaged to each and every device in the
voting universe).

## Approach
1. Model your interpretation of the Bully Algorithm with a state model
2. For each state in your model, define some LED states (e.g., Blue = leader, red = non-leader, green = timeout, etc.)
3. Define the data exchanged in support of the model
4. Using the state-model-to-code approach, implement your leader election with a single identical program running on your set of ESP32s.
5. Initiate leader fails by unplugging an active ESP32 and showing the new leader get elected


## Assignment
1. Bring up a working system
2. Demonstrate booting up as set of devices and leader election
3. Demonstrate leader failure and recovery
4. Demonstrate leader coming back on line
5. Report

## Reference material
- [Wiki Leader Election](https://en.wikipedia.org/wiki/Leader_election)
- [Wiki Bully Algorithm](https://en.wikipedia.org/wiki/Bully_algorithm)
