# Debounce a Switch


<p align="center">
<img src="/docs/images/Button.jpg" width="50%">
</p>
<p align="center">
<i> Push Button Switch</i>
</p>

The kit includes a “push button” switch of the single pole, momentary
type. Depending on the quality of the switch, as the contacts are made
and un-made, there can be a mechanical bounce on the contacts. This
can be problematic for code that samples the state of the button at
high speed and can result in unpredictable behavior for some programs.

In this exercise, you will (a) characterize the bounce on the switch,
and (b) debounce in software.

***NOTE: If you can't get a bounce on the switch, create a short using
two wires instead of the switch. This shoule give you good bounce for
the measurement step.***


<p align="center">
<img src="/docs/images/push-button.jpg" width="50%">
</p>
<p align="center">
<i> Push Button Switch Schematic</i>
</p>


## Assignment/Requirements

1. Connect the switch to one of the ESP32 GPIO pins. Add a pull up
resistor (1M Ohm) (may not be needed) to the input pin. In this mode,
when the button is pushed, the GPIO pin is brought to 0V.

NOTE: you need to set the GPIO pin to input and turn on the ESP32!!

2. Attach the scope (Analog Discovery board) to the GPIO pin and try
to capture the transient when the button is pressed. Duplicate for the
release. Save the screen shot for each. Is there a bounce? What is the
settling time? This time is the minimum time required for the switch
to settle.

3. Write a program to sample the input signal and toggle the LED for
each change in switch state. Incorporate the settling time in your
design.

5. Demonstrate the elimination of switch bounce in a scope trace as a
captured image before an after debouncing. Show a photo of your setup
and including in your Report.md file.

## Reference material
- [ESP32 Technical Reference Manual](https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf)
- [Switch bounce](https://en.wikipedia.org/wiki/Switch#Contact_bounce)
