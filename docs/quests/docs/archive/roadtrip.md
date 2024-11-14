# Roadtrip

Your goal in this quest is to create a robust platform for autonomous
driving by implementing "cruise control" (or maintaining a constant
velocity under perturbations) and collision avoidance (not hitting
things). Hazards that we care about will come from the sides (guard
rails == walls) and from in front (cars, people, deer, cats,
etc.). This reduces to three different paradigms used as building
blocks for driving: (1) a control loop to ramp up to and maintain
speed, (2) sensing and steering, (3) front-facing object sensor and
emergency stop.

<p align="center">
<img src="/docs/images/driving-pleasure.png" width="80%">
</p>
<p align="center">
<i>Car Instrumentation and Track Layout for Driving</i>
</p>

## Description 
The overall approach involves (a) attaching sensors and
the ESP to your vehicle, (b) enabling control using feedback from the
wheel speed sensor to maintain a setpoint, (c) enabling control using
feedback from side range sensors to control steering, and (d)
preventing collisions by detecting objects in front of the car.

An ideal place to test this would be a space with a long corridor or
along a sidewalk next to a building. 

<p align="center">
<img src="/docs/images/driving-cruise.png" width="80%">
</p>
<p align="center">
<i>Velocity and Steering Bounds for Driving</i>
</p>



## Solution Requirements
- Must control steering of the car by maintaining track +/- 15cm
- Must use PID control for maintaining a fixed speed setpoint in
the range of [0.1--0.4 m/s] after start and before stop
- Must stop within 20 cm of waypoint (end of track) without collision (clarification: a collision sensor should be triggered at range less than or equal to 20 cm, stopping the car before collision)
- Start and stop instructions should be issued wirelessly through wireless control
- Must display speed information to alpha display (you can use a second breadboard)


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions

<!--- 4. Investigative question: how would you change your solution if you were asked to provide 'adaptive' cruise control?
--->

## Problem Decomposition
A well-designed solution for this problem is best broken-down into
different parts that are reusable and adaptable for different driving conditions. 
Here is our recommended decomposition: 

1. Interface the ESP32 to the car electronics
   - Bring up the sero control on the ESP (via recipe)
   - Establish calibration (via recipe)

Establish the use of selected sensors on the vehicle
   - Wheel speed
   - Ranging (IR, LIDAR-LED, LIDAR-Lite, Ultrasonic) (note recipe for programming unique I2C address using the LIDAR)

2. Establish control approaches, e.g., 
   - Constant distance from wall(s)
   - Angle of walls
   - Orientation of vehicle
   - Speed/distance/acceleration of vehicle

3. Establish safety rules, e.g., 
   - Stop when detect collision pending (front, side)
   - Stop on wireless command

4. Design your software to satisfy the timing of your control algorithm, e.g., 
   - Accommodate timing limits of sensors (how frequently can you read and process a sensor's data?)
   - Accommodate actuator timing (e.g., how frequently can you change wheel angle?)
   - Set PID timing (dt -- cycle time)
   - Make sure the timing is consistent (e.g., with timers or interrupts)
   - Make sure to check for collisions as a priority activity

Very important: test each subsystem as it is built – don’t wait for
a ‘big bang’ approach to developing your solution.


## Reference Material
- [Recipe for Wiring ESP32 to Buggy](/docs/briefs/recipes/recipe-buggy-interfacing.md)
- [Recipe for Calibrating ESC and Steering Servo -- Buggy](/docs/briefs/recipes/recipe-esc-buggy.md)
- [Recipe for using Multiple LIDAR-Lite V3s on same bus](/docs/briefs/recipes/recipe-lidarlite.md)
- [PWM Design Pattern](/docs/briefs/design-patterns/dp-pwm.md)
- [PID For Wall Tracking and Speed Control Design Pattern](/docs/briefs/design-patterns/dp-pid.md)
<!---
- [Tesla Self-Driving Video](https://youtu.be/tlThdr3O5Qo)
- [F1/10 Video](https://youtu.be/vgEyvazwrU8)
--->

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Controls steering to maintain +/- 15cm from track center |  |  1     | 
| Uses PID for speed control holding a fixed speed setpoint after startup and before slowdown [0.1-0.4 m/s] |  |  1     | 
| Stops within 20 cm of end without collision |  |  1     | 
| Start and stop instructions issued wirelessly from phone, laptop or ESP |  |  1     | 
| Measures wheel speed |  |  1     | 
| Uses alpha display to show current speed |  |  1     | 
| Successfully traverses A-B in one go, no hits or nudges |  |  1     | 
