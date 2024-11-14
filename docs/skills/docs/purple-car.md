# TT Car Motor for the Purple Car

We've picked the "TT Motor" as it is ubiquitous and inexpensive. The
version we have may or may not have pigtails but it's the same
item. The motor is geared down to 200 RPM which is ok, but certainly
not going to impress at the drag strip.  If you can find a faster,
inexpensive motor we will consider for adoption.

The motors run on 3--6V at approx. 1.5A. Best to run from a 5V supply
in our case. We will use a Dual H-Bridge Motor Driver (L293D) to
interface the micro to the motors.

In 2024 we added reflective tags for use with the Optitrack system and
the "covered wagon" was born.


<p align="center">
<img src="/docs/images/hood-up-down.jpg" width="30%">
</p>
<p align="center">
<i>Purple Car / Covered Wagon</i>
</p>

The car locomotes using two wheel motors and a dragging
ball-castor. Forward motion is realized by running both motors in the
positive direction. Backwards is the opposite -- by reversing the
polarity on the motors. The H-bridge allows this control.  Turning is
achieved by delivering different PWM signals into each of the motors,
resulting in differential wheel spin.  The logic is (R: right side
motor, L: left side motor):

| R | L | Outcome |
|:---:|:---:|:-------------------:|
| F | F | Goes forward |
| 0 | F | Goes left |
| F | 0 | Goes right |
| R | R | Goes backward |
| 0 | 0 | Stopped |
| R | F | Spin left |
| F | R | Spin right |


For speed control, your best bet is to vary the power input to the
motors using a PWM signal. The MCPWM is designed for this but there is
also the LEDC control which can be adopted which has a simpler
interface. The example servo code (course example code) uses the MCPWM
APIs. The LEDC example is readily adaptable for TT motor speed
control. See the reference links. You will need to configure a PWM
signal for each motor -- here are the settings.

```
    .duty_resolution = LEDC_TIMER_10_BIT,
    .freq_hz = 50,
    .speed_mode = LEDC_HIGH_SPEED_MODE,
    .timer_num = LEDC_TIMER_0,
    .clk_cfg = LEDC_AUTO_CLK,
```

Note that the PWM frequency should be set to 50Hz. For the LEDC interface, set the duty
resolution to 10 bits and vary duty cycle from 0--1023 for 0--100%. 

## Tips
- The motors draw a lot of current... this taxes the USB power especially from your computer
  - We recommend disconnecting the power to the H-bridge when programming
  - Then disconnect the USB cable from your computer
  - Reconnect the USB cable to your battery
  - Then reconnect the H-bridge to drive the motors
- Bring up one motor at a time. The chip can drive two DC motors
- Refer to the schematic below
- The chip has two Vccs: normally one is high voltage/current to drive the motors, and the other is logic level (3.3V)
- The Vcc on the H bridge does not work with 3.3V; use the USB 5V on both Vcc pins (this is safe because the ESP logic levels are output to the H-bridge chip)
- PWMs connect to the EN pins
- Forward/backward logic connects to the regular inputs
- We are not using the wheel speed sensor in this iteration

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
- [ESP-IDF Motor Control with MC-PWM](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/mcpwm/mcpwm_servo_control)
- [ESP-IDF Motor Control example with LED-PWM](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/ledc/ledc_basic)
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
<i> Motor Wiring</i>
<p align="center">
</p>


