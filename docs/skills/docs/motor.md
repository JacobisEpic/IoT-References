# TT Car Motor for the Purlple Car

We've picked the "TT Motor" as it is ubiquitous and inexpensive. The
version we have may or may not have pigtails but it's the same
item. The motor is geared down to 200 RPM which is ok, but certainly
not going to impress at the drag strip.  If you can find a faster,
inexpensive motor we will consider for adoption.

The motors run on 3--6V at approx. 1.5A. Best to run from a 5V supply
in our case. We will use a Dual H-Bridge Motor Driver (L293D) to
interface the micro to the motors.



## Tips
- The motors draw a lot of current... this taxes the USB power especially from your computer
  - We recommend disconnecting the power to the H-bridge when programming
  - Then disconnect the USB cable from your computer
  - Reconnect the USB cable to your battery
  - Then reconnect the H-bridge to drive the motors
- For the Mac, we sometimes have to hard reboot to reset the USB port...
- Bring up one motor at a time. The chip can drive two DC motors
- Refer to the schematic below
- The chip has two Vccs: normally one is high voltage/current to drive the motors, and the other is logic level (3.3V)
- HOWEVER, since our high voltage is 5V, it seems to work best if both the Vccs are set to 5V. This was validated by experimentation
- It does not work with the Vccs at differtent 3.3V and 5V
- PWMs connect to the EN pins
- Forward/backward logic connects to the regular inputs. 

## Assignment
1. Review the reference material on driving motors with the H bridge
2. Review the ESP-IDF motor control API
3. Wire up your motors according to the guide
4. Develop a test program to run the motors through different states (each motor, fwd, rev, stop, different speeds)
5. Report, show evidence, etc.

## Reference material
- [About H bridges and PWM control](http://www.modularcircuits.com/blog/articles/h-bridge-secrets/h-bridges-the-basics/)
[L293 H Driver Chip](https://cdn-shop.adafruit.com/datasheets/l293d.pdf)
- [Motor Control on Arduino](https://learn.adafruit.com/adafruit-arduino-lesson-15-dc-motor-reversing/overview)
- [ESP-IDF Motor Control with PWM](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
- [L298 Driver Example](https://github.com/espressif/esp-idf/tree/11b444b8f493165eb4d93f44111669ee46be0327/examples/peripherals/mcpwm/mcpwm_brushed_dc_control)

<p align="center">
<img src="/docs/images/h-bridge.jpg" width="70%">
</p>
<p align="center">
<i>H-Bridge Hookup for DC Motors on Car</i>
</p>

<p align="center">
<img src="/docs/images/motor-wiring1.jpg" width="50%">
</p>
<p align="center">
<i> </i>


# Pulse Width Modulation (PWM) Nugget

PWM is a simple modulation protocol typically used in servo control
and also intensity control of LEDs. Compared to analog control, PWM is
useful in that values are either high or low, which is easier to
design as it does not require digital-to-analog (DAC) converters. Here
are some key takeaways as it pertains to the ESP32 and the MCPWM
peripheral.

## Frequency
Changing frequency will affect the period of a complete cycle.

- f1 has a higher frequency but a shorter period than f2.

<p align="center">
<img src="/docs/images/pulses-freq.png" width="80%">
</p>
<p align="center">
<i> Pulses and Frequency</i>
</p>

## Pulse Width

The ESP32 MCPWM peripheral allows you to explicitly change your pulse
width. This affects the pulse width in the time domain and is self
explanatory. Interesting to note is that dependent on your frequency,
your signal will look different **but with the same pulse
width**. Frequency is of less significance in servo control just as
long as the max pulse width fits within the period defined by
frequency.

- Both signals have the same pulse width but the different frequencies

<p align="center">
<img src="/docs/images/pulse-width.png" width="80%">
</p>
<p align="center">
<i> Pulse Width</i>
</p>

## Duty Cycle

The ESP32 also allows you to change the duty cycle of your signal from
0 to 100 percent. This is useful for something like LED intensity
control, where the interest is in some percentage of brightness at a
fixed frequency. Dimming is a result of average intensity over time.

- These are the same signals as above, but they represent different
  duty cycles as a result of different frequencies.

<p align="center">
<img src="/docs/images/duty-cycle.png" width="80%">
</p>
<p align="center">
<i>Duty Cycle</i>
</p>

- Here duty cycle is fixed with different frequencies and as a result
  pulse width is different.

<p align="center">
<img src="/docs/images/duty-cycle-fixed.png" width="80%">
</p>
<p align="center">
<i>Fixed Duty Cycle</i>
</p>
