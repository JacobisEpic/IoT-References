# The Crawler/Buggy -- Prep

In this exercise you convert the buggy/crawler from RC control to ESP32 control.
When this step is complete, the The ESP32 will initially control two servos --
the electronic speed control (ESC) and the steering servo. Later you will add sensors to
create self-driving modes.

In addition to wiring, the car's ESC also requires "calibration" at start up. There is a (very
important) recipe for this. Essentially the speed controller
needs to know the set points (PWM widths) for the limits of "Fast,"
"Stop," and "Fast Reverse." Please review this before you launch your
car off the table.

You will also get to know your buggy/crawler in terms of battery connections
and recharging.

<p align="center">
<img src="/docs/images/crawler.jpg" width="70%">
</p>
<p align="center">
<i>Crawler</i>
</p>

***NOTE: before you power up the car, make sure the wheels are
   elevated. The car can launch off the table if your code is not well
   designed***


## Assignment
1. Wire up the ESP32 to the ESC as a servo and ESC usng the instructions in the [recipe for wiring the buggy](/docs/briefs/recipes/recipe-buggy-interfacing.md)
2. Review the [ESC calibration recipe](/docs/briefs/recipes/recipe-esc-buggy.md) for your car type and adopt the sample code to calibrate the ESC
3. Using your prior experience and code for controlling a servo, write a program to test the steering -- cycle the steering servo from center to left to right and back to center
4. Similarly, write up a program to test the ESC -- to slowly cycle the ESC from stop to forward, to stop, to backwards, to stop


## Reference material
- [Recipe for Wiring ESP32 to Buggy](/docs/recipes/docs/recipe-buggy-interfacing.md)
- [Recipe for Calibrating Buggy](/docs/recipes/docs/recipe-esc-buggy.md)
- [PWM Design Pattern](/docs/design-patterns/docs/dp-pwm.md)
- [ESP example code for servos](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/mcpwm/mcpwm_servo_control)
- [Servomechanism](https://en.wikipedia.org/wiki/Servomechanism)
- [Simple Rotary Servo](https://en.wikipedia.org/wiki/Servo_(radio_control))
- [ESP-IDF Motor Control with PWM](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
- [Buggy Product Description](https://www.nitrorcx.com/51c852-fireblue-24ghz.html)
- [Buggy Product User Manual](https://p11.secure.hostingprod.com/@hobbypartz.com/ssl/ibuyrc/manual/51C852.pdf)
- [Buggy ESC Product Description](https://www.hobbywingdirect.com/collections/quicrun-brushed-system)
- [Buggy ESC Product User Manual](https://www.hobbywing.com/products/enpdf/QuicRunWP1625-WP860-WP1060.pdf)
