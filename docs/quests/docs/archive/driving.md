# Autonomous Driving on a Track

Your goal in this quest is to enable the crawler to drive without
collisions between two endpoints on a road segment, a basic
requirement for autonomous vehicles.  The road segment will be set up
in the lab. Testing can be done elsewhere using a wall as reference.

***Note: please do not use the hallways in Photonics for testing the
   crawlers. We've been banned from PHO due to complaints by some
   cranky people. Alas, not all problems are technical ones.***

## Skill Cluster
- [Crawler](/skills/crawler)
- [MicroLIDAR](/skills/lidar-LED)
- [LIDAR](/skills/lidar-lite)
- [Wheel Speed](/skills/wheel-speed)
- [PID](/skills/pid)

## Description
The overall approach involves (a) attaching sensors and the ESP to the
crawler, (b) enabling control using feedback from the sensors to
manipulate the speed and steering as actuators, and (c) Preventing
collisions. Although this appears to be a trivial case, we need to learn
to crawl before we crank up the speed and introduce corners.

<p align="center">
<img src="/docs/images/driving-new.png" width="25%" />
</p>
<p align="center">
<i> Course Layout</i>
</p>

## Solution Requirements
- Must control steering of the car to maintaining center of track +/- 25cm
- Must use PID control for maintaining a fixed speed setpoint in the range of [0.1--0.4 m/s] after start and before stop
- Must stop within 20 cm of end of track without collision
- Start and stop instructions should be issued wirelessly through laptop
- Must display speed or distance information to alpha display


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question:
Define what you would want in a better sensor for the vehicle. Be very
specific in ***quantifying*** its performance. Please cite materials found on the web to support your response.


## Problem Decomposition
A well-designed solution for this problem is
best broken-down into different parts that each can be adjusted for
next-level tracks. Here is how we think about the decomposition:

1. Establish the use of selected sensors on the vehicle
- Wheel speed
- Ranging (IR, LIDAR-LED, LIDAR-Lite, Ultrasonic)

2. Establish control approaches, e.g., 
- Constant distance from walls
- Angle of walls
- Orientation of vehicle
- Speed/distance/acceleration of vehicle

3. Establish safety rules, e.g., 
- Stop when detect collision pending
- Stop on wireless command

4. Design software algorithm to satisfy timing of control algorithm, e.g., 
- Accommodate timing limits of sensors (they vary)
- Accommodate actuator timing
- Set PID timing (dt -- cycle time)
- Make sure the timing is consistent (e.g., with timers or interrupts)
- Make sure to check for collisions

Very important: test each subsystem as they are built – don’t wait for
a ‘big bang’ approach to developing your solution.


## Reference Material
- [PID Design Pattern](/briefs/design-patterns/dp-pid)
- [Tesla Self-Driving Video](https://youtu.be/tlThdr3O5Qo)
- [F1/10 Video](https://youtu.be/vgEyvazwrU8)

