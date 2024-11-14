# Cruise Control

Your goal in this quest is to create a robust platform for autonomous
driving by implementing "cruise control" (maintaining a constant
velocity) and collision avoidance (not hitting things). Hazzards that
we care about will come from the sides (guard rails == walls) and from
in front (cars, people, deer, cats, etc.). This reduces to three
different paradigms: (1) a control loop to ramp up to and maintain
speed, (2) sensing and steering, (3) front-facing object sensor and
emergency stop.

<p align="center">
<img src="/docs/images/cruise.jpg" width="90%" />
</p>
<p align="center">
<i>Cruise Control</i>
</p>

## Description 
The overall approach involves (a) attaching sensors and
the ESP to your vehicle, (b) enabling control using feedback from the
wheel speed sensor to maintain a setpoint, (c) enabling control using
feedback from side range sensors to control steering, and (d)
preventing collisions by detecting objects in front of the car.

An ideal place to test this would be a space with a long corridor or
along a sidewalk next to a building.


## Solution Requirements
- Must control steering of the car to maintaining center of course +/- 25cm
- Must use PID control for maintaining a fixed speed setpoint in the range of [0.1--0.4 m/s] after start and before stop
- Must stop within 20 cm of end of track without collision
- Start and stop instructions should be issued wirelessly through wireless control
- Must display speed or distance information to alpha display


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: how would you change your solution if you were asked to provide 'adaptive' cruise control?

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
- [PID Design Pattern](/docs/briefs/design-patterns/docs/dp-pid.md)
- [Tesla Self-Driving Video](https://youtu.be/tlThdr3O5Qo)
- [F1/10 Video](https://youtu.be/vgEyvazwrU8)


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

