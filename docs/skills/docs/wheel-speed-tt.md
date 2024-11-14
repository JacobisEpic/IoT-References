# Wheel and Car Speed Sensor

Wheel speed can be measured by counting ticks on a rotating plate
attached to the drive axle of the TT motor driving your car wheel. To
determine speed, you will need to count the ticks as they pass the
sensor per unit time. Along with a known number of ticks in the plate
you will be able to determine wheel RPM.

For a single wheel rolling in a straight line the ground speed (in
m/s) will simply be the RPM X 60 (s/m) X wheel circumference (m). But
if your wheels are turning at different rates without slippage, then
you have another matter.

For our devices, the ticks are sensed using an LED/photo-sensor pair
that is either reflective or transmissive. We have both types, but the
transmissive ones are in the kit. One side generates light and the
other side detects the presence of absence of the light, generating a
pulse high/low.  

Your goal is to get all this operating on your car with a software
module that you can reuse to determine car velocity (speed and
direction).

<p align="center">
<img src="/docs/images/WheelSensorPlate.jpg" width="50%">
</p>
<p align="center">
<i>Wheel Sensor Plate </i>
</p>

## Assignment
1. Figure out how to wire up the optical encoder to your ESP32. This
means controlling the optical sensor (or powering directly), and interfacing the
sensor to the micro. There are different strategies for measuring the
ticks -- timing the gap between pulses or counting the pulses for unit
time. Decide how you want to proceed.

2. Code up your solution and test. Plan to implement two sensors on the vehicle.

3. Attach to the car and demonstrate.

4. (optional) Design a way to calculate the velocity of the car when wheel speeds are different.

## Reference material
- [Sparkfun Guide to Optical Encoder](https://learn.sparkfun.com/tutorials/qrd1114-optical-detector-hookup-guide#example-circuit)
- [ESP32 Pulse Couter](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/pcnt.html)
- [ESP32 Timer](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/timer.html)


<p align="center">
<img src="/docs/images/speed.png" width="50%">
</p>
<p align="center">
<i>Speed</i>
</p>