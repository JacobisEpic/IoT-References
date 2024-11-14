# Use PWM to control power delivery to LEDs

LED brightness can be manipulated by controlling the input power
applied to the LED. Because LEDs are nonlinear to current and voltage
(recall the IV curve of diodes), a clever way to control power is via
PWM which controls power by changing the duty cycle of a fixed
voltage.

<p align="center">
<img src="/docs/images/pwm.gif" width="50%">
</p>
<p align="center">
<i>PWM example (from Instructables.com)</i>
</p>

In this exercise, you will create a circuit to use the PWM output to
drive an LED at different intensity levels. Be mindful not to send a continuous signal (without
cycle), and to pick a frequency of at least 1,000 Hz. Note that one of
the links discusses LED PWM in detail.

One more note -- the PWM we are using is a positive value from 0V to
the positive rail (3.3V). There are forms of PWM that realize
different waveformes that can swing from +V to -V.  The LED is
energized in the range of the Vf voltage of the diode until the
positve rail. If the LED does not light, you may have the LED in backwards.


## Assignment/Requirements

1. Use PWM to drive a single LED of your choice
2. Design and implement console control to set an intensity level from 0 to 9
3. The console value should map to a PWM cycle from (0 to 90%) no cooking.
4. Implement a program cycle to drive the LED in discrete steps through the intensity level (up and down), 
staying in each step for 250 ms
5. Demonstrate your results, writeup and report with a picture and any other evidence.


## Reference material
- [Basics of PWM](https://en.wikipedia.org/wiki/Pulse-width_modulation)
- [ESP32 LED control](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/ledc.html)
- [ESP32 PWM for Motor Control](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
- [PWM Brief](/docs/design-patterns/docs/dp-pwm.md)
- PWM on the ESP32, maximum source current spec (remember, no cooking parts)
- Resistors so that I <= max current mA (I=V/R), V is your source voltage
