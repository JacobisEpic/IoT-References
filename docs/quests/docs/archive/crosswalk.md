# Smart Crosswalk

This problem combines aspects of wireless connected systems with a
safety-critical application -- a true cyberphysical scenario that
requires high reliability. In this application we prioritize safety
over other performance metrics.

The scenario is as follows: Pedestrians will each carry a wireless
device (our ESP32). As they approach the smart crosswalk (SC), their
device connects with the SC. The SC then arbitrates the timing of the
'walk' signal for the crosswalk.  We will assume that there is a
sensor to detect the presence of vehicles in the roadway.

Your task involves creating a state model for this system and
implementing a small scale version as a deliverable.  As always, keep
it simple.

<p align="center">
<img src="/docs/images/crosswalk.png" width="100%" />
</p>
<p align="center">
<i>Smart Crosswalk </i>
</p>

Some assumptions here will be helpful:
- Signals 'A' are hardwired together as are signals 'B'
- A pedestrian approaching from any corner will trigger one of A or B signals but not both
- Each pedestrian will traverse only one side (no turns allowed)
- Pedestrians carry an ESP32, the SC uses a single wired ESP32
- The road sensors each use a wireless ESP32 and are used to detect if
  a car is waiting, but we will use a GPIO input to signal a waiting
  car for each lane.
- Pedestrians are detected by receiving an IR or BLE signal from
- Probably other assumptions you should add


## Assignment
1. Work through the use cases and operating scenarios and make sure you have them all
2. Develop a state based model to characterize the system behavior
3. Prototype the system with the SC as a single ESP32 with 4 GPIO pins
for the lane sensors and an IR RX port for reception. The state machine is implemented here.
4. The ESP32 will need to talk to each pedestrian on a LAN
5. Each pedestrian unit should be able to send a message to the SC indicating A or B crossing (either by BLE or IR)
7. Use the alpha display for diagnostics on state
8. Use timers to ensure that pedestrians are time limited (no starvation)
6. Implement and test
7. Create your assessment metrics
8. Write up a description of how you built your solution. Include
concepts, modules, APIs, tools, etc.
9. Submit a < 90s video of your report. Everyone must be on the video.
10 Optional: in addition to your solution, implement using IFTTT

