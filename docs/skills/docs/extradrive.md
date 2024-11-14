# Multi-Sensor Setup

Navigating in the world often involves multiple sensors. For instance,
camera perception recognizing signs, obstacles, traffic lights, and
lanes. Therefore, cameras are an important sensor for an autonomous
vehicle. An IMU can provide additional context regarding speed and
driving quality. An IMU in addition to the encoder can provide both
redundancy (i.e., important in case a sensor fails!) and
complementarity (i.e., additional information not provided by the
encoder). In this skill, you will be adding a camera view and IMU to
your buggy.

<p align="center">
<img src="/docs/images/multi.jpg" width="80%">
</p>
<p align="center">
<i>Sensor Setup Example</i>
</p>

## Assignment:
- Attach the camera to your vehicle.
- Stream video from the camera on your web browser.
- Attach an IMU and plot its speed estimates in a plot with the encoder speed (for
comparison among the two).
- Include a ‘start’ and ‘stop’ control on the browser, for starting and stopping the vehicle.
This can all be done on a local network (i.e., no DDNS, we do not have to have access
to the website).

## Reference Material:

- [RPi camera](/docs/skills/docs/rpi-camera.md)
- [Accelerometer](/docs/skills/docs/accel.md)
