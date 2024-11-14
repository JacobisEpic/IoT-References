# Stepper Motoo

Stepper motors are yet another motor thing to control. They are
interesting because they operate with discrete steps and it is
possible to rotate them into exact positions by controlling their
"step" inputs. The steps are actually bit patters directed to a set of
coils on the motor. Depending on the bit pattern, the motor moves
forward or backward.  Steppers come in unipolar and bipolar types and
the difference means different ways to step them.

Also notable, stepper motors can hold a position by holding a bit
pattern on the coils. This creates holding torque which can be useful
for some mechanical part to hold a position in spite of
perturbations. One consideration, however, is that sometimes the
stepper can lose count -- essentially be in the wrong position. For
this reason, many stepper based systems have a home position to move a
motor to a reset position. This is what happens when you home the
print head of a 3D printer.

Steppers draw a lot of current and can also be controlled by an H
bridge. Check the type (unipolar or bipolar) and follow the guide to
wiring.

We will use a Dual H-Bridge Motor Driver (L293D) to interface the
micro to the steppers. The particular steppers we have came with their
own hardware interface. You are welcome to use this interfaces as an
alternative.


<p align="center">
<img src="/docs/images/Stepper.jpg" width="50%">
<i>Stepper Motor</i>


## Assignment
1. Review the reference material on driving stepper motors with the H bridge
2. Review the ESP-IDF motor control API
3. Wire up your motors according to the guide
4. Develop a test program to run the motors through different states (each motor, fwd, rev, stop, different speeds)
5. Report, show evidence, etc.

## Reference material
- [L293 H Driver Chip](https://cdn-shop.adafruit.com/datasheets/l293d.pdf)
- [Stepper Motor Control](https://learn.adafruit.com/adafruit-arduino-lesson-16-stepper-motors?view=all)
- [EP-IDF Motor Control(https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
