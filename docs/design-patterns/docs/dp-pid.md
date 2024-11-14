# Design Pattern -- PID Control

Refer to the figure below. We use a discrete version of the same
process executing at interval dt.  r is the setpoint, e is the error.

<p align="center">
<img src="/docs/images/pid.png" width="70%">
</p>
<p align="center">
<i>PID Control Loop from Wiki</i>
</p>

In the algorithm below, dt is the evaluation period, and Kp, Ki, and
Kd are the scale factors for the influence of the proportional,
integral, and differential measurements. You will need to tune Kp, Ki,
and Kd appropriately depending on how much you want to weigh each
parameter of the PID controller.

## PID Algorithm

```c
previous_error = 0
integral = 0

While(1)
{
  error = setpoint - measured_value
  integral = integral + error * dt
  derivative = (error - previous_error) / dt
  output = Kp * error + Ki * integral + Kd * derivative
  previous_error = error
  actuate(output)
  wait(dt)
}

```

Of course, the time cycling should be triggered by a timer and not use a
delay function in which case the pattern is more like this:

```c
Initialize timer for period of dt (100 ms)

On timer interrupt {
  error = setpoint - measured_value
  integral = integral + error * dt
  derivative = (error - previous_error) / dt
  output = Kp * error + Ki * integral + Kd * derivative
  previous_error = error
  actuate(output)     // This is either the servo or the ESC output
}
```
See the example code for setting up a periodic timer like this. 

For steering control on the car we illustrate different ways to compute error signals when wall following.

<p align="center">
<img src="/docs/images/angles.png" width="100%">
</p>
<p align="center">
<i>Steering the Car Trig</i>
</p>


## References
- [Wiki PID Control](https://en.wikipedia.org/wiki/PID_controller)
- [Timer Example](https://github.com/BU-EC444/04-Code-Examples/tree/main/timer-example-new)

