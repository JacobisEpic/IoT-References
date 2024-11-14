# Ingestible "Smart Pill"

A new and exciting medical diagnostic tool is an ingestible sensor
that can capture, log, and transmit biometric data while inside the
body. In this quest we will create the basic functions of this device
using an microcontroller including periodic reading of sensors,
working with analog inputs, playing data onto the console with the
serial interface, and starting to learn about the features of the
RTOS.

<p align="center">
<img src="/docs/images/smartpill.jpg" width="100%" >
</p>

<p align="center">
Smart Pill 
</p>

## Description 

The basic idea is that the smartpill will be activated by the
physician or user and then swallowed by the patient. The device will
then pass through the digestive tract and be discarded (we will not
address here the obvious sustainability issues associated with disposable
electronics).

Along it's way, the device will measure important parameters
supporting it's diagnonitic fuction. Signals will typically be analog,
but we may also yield some logical signals (on/off). These should be
logged or transmitted or both (we will deal with transmission
later). For this exercise the focus is on the reading and
reporting. And we want engineering units.

Here are the behaviors we want to achieve:

- Measure and report temperature in engineering units
- Measure and report light levels in Lux
- Measure and report battery level (need divider circuit)
- Measure and report tilt (as logical value)
- Indicate status on LEDs
- Report every 2 s

In terms of LED signaling, your device should behave as follows:
- Green LED: ready to swallow (light sensor sees light)
- Blue LED: normal sensing (light sensor sees dark), blinks every 2 s
- Red: done sensing (no longer in body -- light sensor sees light)

Meanwhile, data on each input should be displayed as text on the
console I/O (from the ESP32 over the serial channel to your laptop
console window). Data to be reported are displayed in engineering units on the consile

## Solution Requirements
- Your solution should be implemented as a periodic cycle of data reporting 
- A button input or a power restart can start the device (in ready-to-swallow mode)
- The sensing cycle is 2 s

## Assignment
1. Develop a model for the behavior of this system based on the information provided
2. Design and build your solution to meet criteria specified in the rubric
3. Demonstrate your work
4. Reporting as per quest reporting instructions
5. Complete self-assessment rubric

## References

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| 1. Measures light level input from photocell |  |  1     | 
| 2. Measures battery voltage input |  |  1     | 
| 3. Measures temerpature input  |  |  1     | 
| 4. Reports elapsed time to console along with sensor readings  |  |  1     | 
| 5. Measures and reports in Engineering units  |  |  1     | 
| 6. Cyclic design reads and reports inputs every 2s  |  |  1     | 
| 7. Uses hardware interrupt for button input   |  |  1     | 
| 8. Lights up correct LEDs per spec   |  |  1     | 

