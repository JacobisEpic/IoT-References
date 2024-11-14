# Servos

Servos are handy actuator devices that not only provide mechanical
movement but also incorporate feedback control to maintain position
control. This is through built-in position sensing.  If you try to
deflect the output, it only tries harder to reach the target set point
which you control. Servos come in different sizes and types including
linear, continuous rotation, and standard. Our servos are the standard
rotational type that arc through about +/- 90 deg.

Controlling the servo position is by PWM with a "neutral" signal of
1.5 ms width at a frequency of about 50 Hz (in the range of 40 to 200
Hz). In some cases, such as ESCs (electronic speed control), the
initial PWM signal is treated as the neutral state at startup.
Increasing the pulse width to 2ms or decreasing to 1 ms affects the
output rotational position.

The code example in the ESP-IDF distribution is where to start.
The servo has bounds of +/- 90 deg for a 180 deg range. We find
that the signal input pulse width is the key parameter and with some
experimentation may be in the range of 700--2300 us (0.7--2.3
ms). However, you'll need to fine tune the min and max pulse width to
your servos (they all behave slightly different). The example code
also provides a function to convert from angles to pulse width.

<p align="center">
<img src="/docs/images/Servo.jpg" width="25%">
</p>
<p align="center">
<i> Servo </i>
</p>

## Assignment
1. Review the reference material on servos and PWM in the design pattern. This breaks down the code example and links to current code. 
2. Figure out how to wire one or more servos to your ESP32
3. Develop a test program to set the servo to a specific angle with keyboard input.
4. Report, show evidence, etc.

## Reference Material
- [PWM Brief](/docs/design-patterns/docs/dp-pwm.md)
- [ESP-IDF example servo code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/mcpwm/mcpwm_servo_control)
- [Example servo code with additional comments](https://github.com/BU-EC444/04-Code-Examples/tree/main/servo)
- [Servomechanism](https://en.wikipedia.org/wiki/Servomechanism)
- [Simple Rotary Servo](https://en.wikipedia.org/wiki/Servo_(radio_control))
- [ESP-IDF Motor Control with PWM](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
