# PID Control Using the Micro

PID - proportional, integral, differential refers to holding a set
point based on error measurements.  

<p align="center">
<img src="/docs/images/pid.png" width="60%">
</p>
<p align="center">
<i>PID Control Loop from Wiki</i>
</p>

You may not remember your control theory (see the wiki for a
refresher), but the key ideas are:

- The PID controller tries to maintain some setpoint value that is
  ideally measureable (e.g., vehicle speed for cruise control set a 65 MPH)
- The micro measures this value and determines deviations (errors) -- is the 
car slower are faster than 65 MPH?
- If it is faster (an "error" between the set point (65) and the measured 
(say 68)), then the controller increases the power to the engine (presses gas pedal).
- If the car is slower, it does the opposite
- The aforementioned is proportional control -- the amount of the corrective 
signal is proportional to the error.
- The differential part relates to how fast the error is generated 
- The integral part relates to steady state error that recurs each time it
is evaluated.
- When combined, the P, I, and D overcome different
behaviors that might be introduced by the car (inertia, delays,
acceleration, etc.) and setting parameters is the basis for control
system design.
- On a micro we can implement a discrete PID controller with a regular
evaluation cycle that is a time scale in relation to the problem at
hand. For example, controlling a car will require a shorter evaluation
period (order ms) whereas temperature control of a 3D printer head will be slow (order seconds).

We have posted a design pattern for implementing a PID loop as code in the
briefs section.

For this skill, we will create a PID loop with only proportional
control, and the actuator will be a human (we do this later 
with the car as actuator). See the diagram below.

<p align="center">
<img src="/docs/images/pid-leds.png" width="70%">
</p>
<p align="center">
<i>Proportional Control With LEDs</i>
</p>

Wire up 4 LEDs as shown. Attach your favorite range sensor and reuse
your range code. Using the PID design pattern, impelment a timing loop
with a 100ms period. (We recommend using an interrupt for this timer,
but it is not essential for this skill.) On each cycle, calculate the
error signal and evaluate. Use the following rules:

- If the error < 0, then turn on the red LED
- If the error = 0, then turn on the green LED
- If the error > 0, then turn on the blue LED

Evaluate your solution using some setpoint (say 50 cm). If you move
above or below the setpoint, you should be demonstrating the feedback.


## Assignment
1. Bring up the range sensor
2. Code a proportional control algorithm (see design pattern) with a setpoint at a distance within the sensor's range
4. Implement and demonstrate
5. Report

## Reference material
- [PID design pattern](/docs/design-patterns/docs/dp-pid.md)

