# Venus Rover

When it comes to planetary exploration, Mars gets all the attention. Here
we consider Venus instead.

Venus is inhospitable to humans, but we hope to visit and collect some
microbial life forms (Venusians) for further study. We'll say that they live in
hot springs. Our mission is to land, deploy our rover to drive to the
hot springs, collect the Venusians, drive back to the ship, and then
return to Earth. This is illustrated below.

<p align="center">
<img src="/docs/images/venus1.jpg" width="100%">
</p>
<p align="center">
<i>Venus Exploration Scenario</i>
</p>

Your goal in this quest is to create a robust platform for autonomous
driving that makes the round trip between the ship and the hot
springs. You will implement (1) "cruise control" (or maintaining a
constant velocity under perturbations), (2) "turn-around" (reversing
the direction of the vehicle), and (3) "collision avoidance" by
detecting obstructions and driving around them. Of course you need to
get from A to B and back to A, so some navigation is required.

<p align="center">
<img src="/docs/images/venus2.jpg" width="100%">
</p>
<p align="center">
<i>Schematic of Ship-to-Hot-Springs Round Trip</i>
</p>


## Description

The overall approach involves (a) attaching sensors and the ESP to
your vehicle, (b) enabling control using feedback from the wheel speed
sensor to maintain a speed setpoint (driving the vehicle motor), (c)
using range sensors to detect and avoid objects, and (d) maintaining
forward progress towards each waypoint (A and B).
An ideal place to test this would be a space with a long corridor. 


<p align="center">
<img src="/docs/images/venus3.jpg" width="25%">
</p>
<p align="center">
<i>Possible Sensor Locations</i>
</p>


## Solution Requirements
- Successfully makes A--B--A trip in reasonable time window
- No collisions with obstructions
- Start and stop instructions should be issued wirelessly through wireless control
- Can use automatic or manual control at turnaround (you can implement a turning
  algorithm or do this with remote control of steering)
- Displays elapsed time on alpha display
- Constant speed except when doing turns or collision avoidance


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions

## Problem Decomposition
A well-designed solution for this problem is best broken-down into
different parts that are reusable and adaptable for different driving conditions. 
Here is our recommended decomposition: 

1. Interface the ESP32 to the car electronics
   - Bring up the sero control on the ESP (via recipe)
   - Establish ESC calibration (via recipe)

2. Establish the use of selected sensors on the vehicle
   - Wheel speed
   - Ranging (LIDAR, Ultrasonic, or IR) 

3. Establish control approaches, e.g., 
   - Constant distance from wall(s)
   - Angle of walls
   - Orientation of vehicle
   - Speed/distance/acceleration of vehicle
   - Changing from manual to self-driving control

4. Establish safety rules, e.g., 
   - Stop when detect collision pending (front, side)
   - Stop on wireless command

5. Design your software to satisfy the timing of your control algorithm, e.g., 
   - Accommodate timing limits of sensors (how frequently can you read and process a sensor's data?)
   - Accommodate actuator timing (e.g., how frequently can you change wheel angle?)
   - Set PID timing (dt -- cycle time)
   - Make sure the timing is consistent (e.g., with timers or interrupts)
   - Make sure to check for collisions as a priority activity

Very important: test each subsystem as it is built – don’t wait for
a ‘big bang’ approach to developing your solution.


## Reference Material
- [Recipe for Wiring ESP32 to Buggy](/docs/recipes/recipe-buggy-interfacing.md)
- [Recipe for Calibrating ESC and Steering Servo -- Buggy](/docs/recipes/recipe-esc-buggy.md)
- [Recipe for using Multiple LIDAR-Lite V4s on same bus](/docs/recipes/recipe-lidarlite-v4.md)
- [PWM Design Pattern](/docs/design-patterns/dp-pwm.md)
- [PID For Wall Tracking and Speed Control Design Pattern](/docs/design-patterns/dp-pid.md)

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Uses PID for speed control holding a fixed speed setpoint after startup and before slowdown |  |  1     | 
| Stops within 20 cm of end without collision |  |  1     | 
| Start and stop instructions issued wirelessly from phone, laptop or ESP |  |  1     | 
| Measures wheel speed |  |  1     | 
| Uses alpha display to show elapsed time |  |  1     | 
| Successfully traverses A-B in one go, no hits or nudges |  |  1     | 
| Successfully reverses direction (auto or remote control), no hits or nudges |  |  1     | 
| Successfully traverses B-A in one go, no hits or nudges |  |  1     | 
| No collisions with obstructions |  |  1     | 
