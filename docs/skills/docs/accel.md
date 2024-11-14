# Triple-axis Accelerometer

<p align="center">
<img src="/docs/images/accel.jpg" width="60%">
</p>
<p align="center">
<i> Accelerometer</i>
</p>

## Description
In your team kit is a handy-dandy digital accelerometer, the
ADXL343. This microelectromechanical system (MEMS) device measures
acceleration in 10/13 bit resolution for three axes as well as
providing a couple of motion interrupts. With this information, you
can design a system to record motion (activity) and tilt
(orientation). The ADAXL343 has two interfaces: I2C and SPI. In the
alphanumeric skill, we told you not to fret and that you'll get your
chance to write I2C code, well, now's your chance. (We will ignore the
SPI bus as I2C is simpler and sufficient.)

## Helpful Hints
- We will provide you with base code to start
- Work modularly: figure out I2C, then read acceleration, then convert to tilt angles
- I2C requires pull up resistors (the data lines are pulled up and
down during communication), some pins on the ESP32 have internal
pull-up resistors, some don't, be mindful.
- Everything you need is in the reference material section linked below

## Assignment
1. Wire up the ADXL343 accelerometer on your breadboard with the ESP32
2. Create a module that allows you to read acceleration in the x, y, and z axes
3. Write a function to convert static acceleration values into tilt data
4. Report evidence of completion in your repository

## FAQ

1. How do I read acceleration data when it is in two bytes (16 bits)?
Answer: There's a lot of talk in the data sheet about right justified and left justified data format. If you have default values, the data is right justified. It is also in 2's compliment (signed integer). Steps to reassemble:
	- Read each value (byte) into an integer (signed or unsigned)
	- Combine the two values into a signed-word (16 bit) by ORing the LSB with the MSB shifted to the left by 8
	- Return this as a signed 16 bit word
	- Cast the result into a float before multiplying by the scale factor (mg/bit). If your scale factor is right, the results should show the right gravity value for the range setting
2. How do I know if my values are correct?
Answer: Acceleration is measured in terms of gravity. If your device is set on a flat service and not moving, one of your axes should read 9.8 as in 9.8  m/s^2 (aka gravity).
 
3. Do I need to read two bytes at once with the read multiple bytes command?
Answer: This depends on the sampling speed you desire.


## Reference Material
- [I2C Brief](/docs/design-patterns/docs/dp-i2c.md)
- [ADXL343 Base Code](https://github.com/BU-EC444/04-Code-Examples/tree/master/i2c-accel)
- [ADXL343 Datasheet](https://cdn-learn.adafruit.com/assets/assets/000/070/556/original/adxl343.pdf?1549287964)
- [Adafruit Learn Guide on the ADXL343](https://learn.adafruit.com/adxl343-breakout-learning-guide/overview)
- [Adafruit Example Code](https://github.com/adafruit/Adafruit_ADXL343)
- [Sparkfun I2C](https://learn.sparkfun.com/tutorials/i2c)
- [ESP-IDF I2C API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/i2c.html)
- [ESP-IDF Example code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2c)
- [Tilt Sensing](https://wiki.dfrobot.com/How_to_Use_a_Three-Axis_Accelerometer_for_Tilt_Sensing)
- [Extra reading on realizing a pedometer](https://cdn-learn.adafruit.com/assets/assets/000/070/557/original/pedometer-design-3-axis-digital-acceler.pdf?1549288142)

