# Building a Stopwatch

The ESP32, like many microcontrollers, has a built-in timer
functionality. In this exercise you will create a simple digital stopwatch
using the timer.

This skill requires the use of timer interrupts rather than using a
simple delay of 1,000ms.

<p align="center">
<img src="/docs/images/alpha.jpg" width="50%">
</p>
<p align="center">
<i>Alphanumeric Display for Stopwatch</i>
</p>

Best to have a look at the ESP32 API for the timer, our example timer code,  and the example
code on the ESP-IDF Github site (links below).

## Assignment

1. Your stopwatch shall employ the pushbutton, the alphanumeric display, and
  the interrupt-driven timer function 
2. On button press, the timer should start counting up in seconds
(the button can be detected by polling the GPIO or by configuring the the GPIO for interrupt as you have done before)
3. Additional presses of the button should restart the counter at zero
4. The alphanumeric display should display the current count in seconds.
5. The display shoud wrap modulo 16 ( ...14, 15, 00, 01,...)
6. Report out as usual


## Reference Material
- [Timer Interrupts Design Pattern](/docs/design-patterns/docs/dp-timer.md)
- [ESP32 Guide: General Purpose Timer](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/gptimer.html)
- [ESP-IDF Github Timer Example](https://github.com/espressif/esp-idf/tree/17ac4ba/examples/peripherals/timer_group)
