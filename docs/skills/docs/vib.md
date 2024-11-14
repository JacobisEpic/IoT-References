# Vibration switch (hardware interrupts)

<p align="center">
<img src="/docs/images/vib.jpg" width="60%">
</P>
<p align="center">
<I>Vibration Switch </i>
</p>

In this skill, you will bring up a tilt switch that is triggered by
vibration (a metal spring joins and closes the circuit when there's
motion). We will set up our switch in pull-up mode. That is, when the
switch is open, it is pulled HIGH to 3.3V. Do this the usual way with
a 10k pull-up resistor with the other end tied to ground. Therefore,
when the vibration switch is engaged, the signal is pulled down to
ground -- see schematic below.

<p align="center">
<img src="/docs/images/switch-pullup.jpg" width="50%">
</p>
<p align="center">
<i> From Sparkfun</i>
</p>

### Debouncing

We have not really explored the behavior of the vibration sensor, but
we expect that it will trigger multiply as we see with a switch
bounce. Thus it will be necessary to manage multiple bounces with
filtering or by using interrupts and filtering.

## Assignment
1. Wire up the vibration switch with a pull-up resistor
2. Program a hardware interrupt to light up the onboard LED when tapped
3. Optional, but informative: put a scope on the switch and capture signal that occurs when you tap the sensor
4. Eliminate switch debounce so that a tap is only counted once, print taps on console.
5. Report evidence of completion in your repository


## Reference material
- [Design Pattern for Interrupts](/docs/design-patterns/docs/dp-interrupts)
- [Vibration Switch](https://www.adafruit.com/product/1766)
- [Switch bounce](https://en.wikipedia.org/wiki/Switch#Contact_bounce)
- [Sparkfun Pull-up Resistor](https://learn.sparkfun.com/tutorials/pull-up-resistors)
- [ESP32 GPIO Interrupt Code Example](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/gpio)
- [ESP32 Interrupt Allocation](https://esp-idf.readthedocs.io/en/latest/api-reference/system/intr_alloc.html)
