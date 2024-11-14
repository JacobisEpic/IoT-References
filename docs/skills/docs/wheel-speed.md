# Wheel and Car Speed Sensor

Wheel speed can be measured by counting ticks on a rotating plate
attached to one of the wheels on the crawler. A printed black and
white pattern attached to the side of one of the wheels works
well. You will need to figure out how to mount your sensors on the
crawler chassis.  To determine speed, you can count changes in
intensity at the sensor output per unit time. Along with a known
number of tranisitons on the plate you will be able to determine wheel
RPM.

For a single wheel rolling in a straight line, the ground speed (in
m/s) will be the RPM X 60 (s/m) X wheel circumference (m). This
assumes no slippage. For the crawlers, we measured 62 cm as
circumference. This yields about one pulse per 10cm for the 6-way
encoder disk. You could also try a different encoder disk.

In our setup, the pattern is sensed using an LED/photo-sensor pair
that is reflective. One side generates light and the other side
detects the reflection. White reflects more light than black allowing
you to discriminate the pattern.

Your goal is to get all this operating on your car with a software
module that you can reuse to determine car speed. For the buggy, save
the encoder gif and print scaled to 30% to fit the buggy wheel.

<p align="center">
<img src="/docs/images/encoder.gif" width="20%">
</p>
<p align="center">
<i> Encoder Pattern</i>
</p>

## Assignment
1. Figure out how to wire up the optical encoder to your ESP32. This
means controlling (powering) the optical emitter (LED), and interfacing the
sensor to the micro. There are different strategies for measuring the
changes in reflected light -- timing the gap between pulses or counting the pulses for unit
time. Decide how you want to proceed.
2. Code up your solution and test. Plan to implement a single sensors on the vehicle.
3. Attach to the car and demonstrate.

<p align="center">
<img src="/docs/images/wheelspeed3.jpg" width="50%">
</p>
<p align="center">
<i>Sensor Mounting</i>
</p>
<p align="center">
<img src="/docs/images/wheelspeed2.jpg" width="50%">
</p>
<p align="center">
<i>Sensor Mounting </i>
</p>


## FAQ
1. We seem to have trouble controlling the car at slow speeds.
Answer: try using a wheel speed encoder template with more ticks (try 12 cycle pattern instead of 6). 


## Reference material
- [Sparkfun Guide to Optical Encoder](https://learn.sparkfun.com/tutorials/qrd1114-optical-detector-hookup-guide#example-circuit)
- [ESP32 Pulse Couter](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/pcnt.html)
- [Rotary Encoder Example](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/pcnt/rotary_encoder)
- [ESP32 Timer](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/gptimer.html)
- [Wheel Speed Encoder Generator](https://www.thingiverse.com/thing:1527/files)
- [Wheel Speed Encoder Template](/docs/images/encoder.gif)

