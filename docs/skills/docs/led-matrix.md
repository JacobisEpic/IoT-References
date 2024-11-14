# Write a Module in C to Drive the 8x8 LED Matrix

<p align="center">
<img src="/docs/images/Dotarray.jpg" width="50%">
</p>
<p align="center">
<i> LED Dot Array Unit</i>
</p>

This exercise is to design and implement a driver for the 8x8 LED
matrix. Although there are hardware mechanisms to simplify this goal,
the intent is to gain experience in translating symbol values into bit
values with a spatial representation of the symbols (characters). This
is all data/bit manipulation (bit twiddling) that can be done cleverly.

Having a hardware output display device is especially important as a
diagnostic tool when programming embedded systems of this type. You
will use this function later in the course, or if the wiring becomes a
burden, the I2C alphanumeric display.

## Assignment/Requirements

1. Able to write two arbitrary ASCII characters to the display
2. Display continuously until overwritten
3. Solution is modular – can be reused in other assignments
4. Demonstrate with text entered from console
5. Optional: Display longer scrolling ASCII strings.

As part of this exercise you will need to wire up the LED matrix with
your micro and establish how to send patterns to the matrix. the links
below connect to specs on the provided hardware components:

<p align="center">
<img src="/docs/images/dot-array.jpg" width="50%">
</p>
<p align="center">
<i> Example Circuit</i>
</p>


## Reference material
- [LED Matrix](https://cdn-shop.adafruit.com/datasheets/KWM-30881XVB.pdf)
- [74HC595 Shift Register](https://cdn-shop.adafruit.com/datasheets/sn74hc595.pdf)
- [Shift register techniques](https://www.arduino.cc/en/Tutorial/ShiftOut)
- Resistors so that I <= 20mA (I=V/R), V is your source voltage
