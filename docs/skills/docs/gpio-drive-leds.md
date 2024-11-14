# Use GPIO to Drive LEDs

In this exercise, you will establish input or output on a set of GPIO
pins and write code to drive multiple LEDs.

<p align="center">
<img src="/docs/images/LEDs.jpg" width="20%">
</p>
<p align="center">
<i>Simple R,G,B,Y LEDs</i>
</p>

## Note: you will set up a ***new*** project using the ESP code base.

This is done most effectively by copying files from an example in the
ESP distro to your working directory. Your PATH variables will need to
include both the ESP distro and your working directory, and you will
need to bring over the file structure and config files of the example
code. See the ESP develoment guide on how to initiate a folder for a
new project or checkout the design pattern for [Setting up a New
Project](/docs/design-patterns/docs/dp-project.md).



## Assignment
1. Goal is to toggle GPIO signals on and off to control a set of LEDs
2. Wire up 4 LEDs without cooking anything
   - use 3.3V from the ESP32 and plug ESP32 into an USB power source
   - the ESP32 board will source up to ~250mA of the total of 500mA at 3.3V)
   - Use resistors so that I <= max current mA (I=V/R), V is your source voltage (use 330 ohm)
3. Make a blink-type program that illuminates the LEDs as follows (LED positions 4, 3, 2, 1)
   - Period is 1s
   - All LEDs off
   - LED 1 on (1 s)
   - LED 1,2 on
   - LED 1,2,3 on
   - LED 1,2,3,4 on
   - Binary countdown, 1s each, back to all LEDs off
   - Repeat

4. Take photos and write up a description in Report.md on github

<p align="center">
<img src="/docs/images/led-example.jpg" width="50%">
</p>
<p align="center">
<i>Example Wiring to ESP32. Note: can use different pins than shown</i>
</p>

<p align="center">
<img src="/docs/images/gpio-leds.jpg" width="70%">
</p>
<p align="center">
<i>Schematic (LEDs connect to available GPIO pins)</i>
</p>


## Reference material
- [Setting up a New Project](/docs/design-patterns/docs/dp-project.md)
- [Sample project](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#example-project)
- [Basic LED information](https://en.wikipedia.org/wiki/Light-emitting_diode)
- [Huzzah32-ESP32](https://cdn-learn.adafruit.com/downloads/pdf/adafruit-huzzah32-esp32-feather.pdf)
- [Powering the ESP32](/docs/utilities/docs/powering-esp.md)
- [Resistor Color Code](https://en.wikipedia.org/wiki/Electronic_color_code)
