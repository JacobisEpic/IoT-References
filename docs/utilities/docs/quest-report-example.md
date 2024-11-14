# Quest: 8x8 Dot-Array Display 

Authors: Shohei Ohtani

Date: 2024-09-01

### Summary

In this quest we wired a 8x8 LED Dot-Array to the ESP32
to enable writing aphanumeric characters as a display unit.


### Solution Design

We used a shift registers to deliver data to the dot matrix device.
This allows us to use 3 GPIO pins on the
micro-controller to control 64 LEDs. In this example, we used the
dot-array display one line of the dot-array at a time to test out the
functionality.

We used the SN74HC595 shift register device based on
the Arduino Shift Register Tutorial for the approach
to our solution.  The pins used for communications are:

- ST_CP of 74HC595 --> pin 33 of ESP32
- DS of 74HC595 --> 27
- SH_CP of 74HC595 --> pin 12 of ESP32

Since the ESP32 has 3.3 V logic level, current limiting resistors (220
ohms) were used to limit the current to the LED matrix.  Important to
note is that the shift registers operate on a rising edge, so it was
important to send bits in on the rising edge of the clock pin. The
latch pin was used to disable the display when transmitting data.

<p align="center">
<img src="/docs/images/dot-array.jpg" width="50%">
</p>
<p align="center">
<i>Dot Array Implementation</i>
</p>


(The length of this section will be depend on the scope of the quest.)

### Quest Summary

All in all, this was a small quest (really just a skill). But the
resulting product allows us to display diagnostic information onto a
dot matrix device which is pretty useful in debugging.

### Supporting Artifacts
- Link to video technical presentation
- Link to video demo 

### Self-Assessment Based on Rubric


| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Sent an ASCII character from the console to the display | 1 |  1     | 
| Holds a character on the display until refreshed | 1 |  1     | 
| When two characters are sent for display, each one is displayed for 1s then it toggles to the other | 1 |  1     | 

### AI and Open Source Code Assertions

- We have documented in our code readme.md and in our code any software that we have adopted from elsewhere
- We used AI for coding and this is documented in our code as indicated by comments "AI generated" 
