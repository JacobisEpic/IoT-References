# Alphanumeric Display

<p align="center">
<img src="/docs/images/tdcl-display.jpg" width="60%">  
</p>
<p align="center">
<i>Example Ouput from Alphanumeric Display </i>
</p>

## Description   

We use the [Adafruit 14-Segment Alphanumeric
LED](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing)
which works with the ESP32. But it will need to be breadboarded along
with the ESP32.


Each digit on the alphanumeric display is 14 LED segments plus a
decimal point LED. With different combinations of the 14 segments
turned on and off you can form most letters and numbers. But
controlling all the segments individually is better done via off-board
logic with signals/commands sent in a more concise way (fewer
connections) via a communication bus such as I2C or SPI. The
alphanumeric display included in your kit uses I2C. We use the
Adafruit 14-segment alphanumeric display which is designed to mate
with the ESP32 except that our devices have the wrong headers. You
should connect the LED board and the ESP32 onto a breadboard with
jumpers. We provide the [I2C
interface](https://github.com/BU-EC444/04-Code-Examples/tree/main/i2c-display)
for this
skill. However, future assignments may ask you to develop the I2C API
yourself.

### Helpful Hints
- Spend some time to build a clean wiring job as this display will be a
useful debugging tool for you.
- I2C requires pull up resistors (the data lines are pulled up and
down during communication), some pins on the ESP32 have these
internally. The SCL and SDA pins have internal pull ups.  
- The LED driver uses MSB.
- As for the software, the most useful tool will be to be able to write
arbitrary ASCII characters onto the display. For example, to flag
various states or breakpoints in your programs. This greatly aids
debugging when you do not have a console attached to a device.


### Wiring for the Huzzah board
The pins are not labeled on the display board as it is intended to plug directly into the headers
on the Huzzah32 board. The pic below shows a top view when connecting jumpers.

<p align="center">
<img src="/docs/images/alpha.png" width="50%">
</p>
<p align="center">
<i>Pin Information for Alpha Board</i>
</p>

## Assignment
1. Wire up the alphanumeric display on your breadboard with the ESP32
2. Create a module that allows you to write ASCII characters in a string (up to 16 characters) to the
display from the console. If there are more than 4 characters, the display should scroll automatically. 
3. Build, test, demo
4. Report evidence of completion

## Reference Material
- [Alphanumeric Brief](/docs/briefs/docs/alphanumeric.md)
- [Alphanumeric I2C code](https://github.com/BU-EC444/04-Code-Examples/tree/main/i2c-display)
- [Bitmap Guide](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing/usage#library-reference-4-14)
- [Bitmap Cheat](https://github.com/adafruit/Adafruit_LED_Backpack/blob/master/Adafruit_LEDBackpack.cpp)
- [Adafruit 14-Segment Alphanumeric LED](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing)
- [Matrix Driver](https://cdn-shop.adafruit.com/datasheets/ht16K33v110.pdf)
- [Adafruit Guide](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing?view=all)
- [Sparkfun I2C](https://learn.sparkfun.com/tutorials/i2c)
- [ESP-IDF I2C API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/i2c.html)
- [ESP-IDF Example code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2c)
- [ASCII Tables](https://en.wikipedia.org/wiki/ASCII)
