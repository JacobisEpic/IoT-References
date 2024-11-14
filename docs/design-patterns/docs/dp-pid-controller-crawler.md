# PID Controller
We seek to enable predictable and controlled behavior on the
Crawlers. There are several functions we can address that can benefit
from feedback.

1. Speed control – by sensing the wheel speed, the ESC (motor speed
control) can be adjusted to sustain a set-point in spite of
perturbations (classic cruise control)
2. "Adaptive cruise control" – by measuring the distance to another
crawler, one crawler can follow at a same speed
3. Distance to wall control – by measuring the distance to the wall at
a single point, a crawler can make adjustments to position to correct
deviations in the measured error from a set-point. This requires some
thought as the crawler cannot move in arbitrary directions.
4. Angle to wall control – by measuring the distance to the wall at
multiple points, the angle to the wall can be the controlled function.

Sensors: Range finder or wheel rotation<br>
Actuator: electronic speed control (servo) on crawler, steering servo

Programing

<p align="center">
<img src="/docs/images/pid_pic_1.png" width="80%">
</p>
<p align="center">
<i>From Wiki PID Controller</i>
</p>

### Steps:

1. Implement target code for PID controller
2. Establish gain parameters for P, I, D
3. Tune P, I, D gain parameters
4. Demonstrate – use input (keyboard) to specify a range set-point, have crawler achieve set-point

### Pseudo-code from Wiki (PID Controller)

This code will work with any of the options above if properly framed.

```
previous_error = setpoint - process_feedback
integral = 0
start:
  wait(dt)
  error = setpoint - process_feedback
  integral = integral + (error*dt)
  derivative = (error - previous_error)/dt
  output = (Kp*error) + (Ki*integral) + (Kd*derivative)
  previous_error = error
  goto start
```

<p align="center">
<img src="/docs/images/pid_pic_2.png" width="80%">
</p>
<p align="center">
<i></i>
</p>



### Distance to Wall control

<p align="center">
<img src="/docs/images/pid_pic_3.png" width="80%">
</p>
<p align="center">
<i></i>
</p>


Set-point (SP) is the desired distance in this recipe. Process
variable (PV) is the current distance, measured by some range sensor
and feedback to the closed control loop. So

```
error = setpoint - process_feedback
```

In discrete time, the integration can be estimated as the accumulated
sum:

```
integral = integral + (error*dt)
```

The derivative can be estimated by the change rate of the error:

```
derivative = (error - previous_error)/dt
```

The output of the PID controller is the Manipulated variable (MV),
which is the speed, the signal to ESC/Crawler. Then the crawler
updates the PV.

<p align="center">
<img src="/docs/images/pid_pic_4.png" width="80%">
</p>
<p align="center">
<i></i>
</p>


## Angle to wall control

One strategy for steering is to maintain a fixed set point on some
error signal. For example, the distance to one (or both) walls can be
maintained. This can be achieved with one or more sensors. For
example, in the illustration below, the difference, delta, can be
measured by using two sensors that determine the orientation of the
crawler with respect to a single wall. This delta can be controlled to
maintain a value of zero as the target set point. Variations of this
concept can be applied when two walls are involved.


<p align="center">
<img src="/docs/images/pid_pic_5.png" width="80%">
</p>
<p align="center">
<i></i>
</p>

At this point it should become clear that the crawler does not move
arbitrarily in 2D. In order to move the vehicle closer to the wall one
needs to move it forward while controlling the steering servo. There
are several strategies. Here is one:

- Operate at a fixed speed but change the steering at a known angle
  for a known duration. Change displacement from center line by right
  then left turn(or L then R turning): turn for unit time, then turn
  back. Calculate displacement for this case depending on angle and
  speed.

## Reference materials

- <http://code.activestate.com/recipes/577231-discrete-pid-controller/>
- <http://www.atmel.com/Images/doc2558.pdf>
- <http://www.mathworks.com/help/simulink/slref/pidcontroller.html>
- <http://www.expertune.com/tutor.aspx>
- <http://en.wikipedia.org/wiki/PID_controller>
