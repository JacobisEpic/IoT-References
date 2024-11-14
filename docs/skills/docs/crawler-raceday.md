# The Crawler -- Prep

In this exercise you put the wheels on the crawler and bring it up
under ESP32 control (this year we are not going to do the race day due
to logistical issues). The ESP32 will initially control two servos --
the electronic speed control and the steering servo.

The ESC also requires "calibration" at start up. There is a (very important) design
pattern for this. Essentially the speed controller needs to know the
set points (PWM widths) for the limits of "Fast," "Stop," and "Fast
Reverse." Please review this before you launch your car off the table.

You will also get to know your crawler in terms of battery connections
and recharging.

<p align="center">
<img src="/docs/images/crawler.jpg" width="80%">
</p>
<p align="center">
<i>Crawler</i>
</p>

## Assignment (Race Day)
1. Attach the wheels -- special wrench to do so 
2. Familiarize yourself with the crawler, remote control,
battery, charging, etc.
3. Test drive in the classroom
4. Save your battery for the race


## Assignment (Post Race Day)
1. Wire up the ESP32 to the ESC as a servo
2. Wire up the ESP32 to the crawler steering servo
3. Write a program to test the steering -- cycle the steering servo from center to left to right and back to center
4. Write up a program to calibrate the ESC (see design pattern)
5. Write up a program to test the ESC -- to slowly cycle the ESC from stop to forward, to stop, to backwards, to stop


## Reference material
- [ESC Design Pattern](/docs/design-patterns/docs/dp-esc)

