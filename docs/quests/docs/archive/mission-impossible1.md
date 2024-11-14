# "Mission: Impossible"

Tom Cruise breaks into a high-security server room in this 1996 action
thriller. But we're committed to foiling his hack. In this quest you will
setup sensors to detect the break-in. These include heat (thermistor),
light (photocell), and tripwires (contact breaks). The quest involves
periodic reading of sensors, reading analog signals, playing data
onto the console with the serial interface, and starting to learn
about the features of the RTOS.

<p align="center">
<img src="/docs/images/tom-cruise.jpg" width="50%" >
</p>

<p align="center">
Mission: Impossible (Paramount Pictures)
</p>

<p align="center">
<img src="/docs/images/vault.jpg" width="50%" >
</p>

<p align="center">
Our Secure Vault Monitoring System
</p>

## Description 

For this quest we will use a photocell to detect changes in light
level caused by an intruder occluding overhead lights. Similarly, we
use a thermistor to detect changes in room temperature (for example,
caused by the physical exertion of character Ethan Hunt). Lastly, we
will simulate a floor contact sensor using a pushbutton (if he touches
the floor, an alarm is triggered).

<p align="center">
<img src="/docs/images/mi-sensors.jpg" width="50%" >
</p>

<p align="center">
Sensors and LEDs for the Secure Our Secure Vault Monitoring System
</p>


In terms of alarm reporting, your solution should turn on LEDs
indicating each type of fault: green (all clear), red (temperature
change), yellow (light change), blue (floor touch). Meanwhile, data on
each input should be displayed as text on the console I/O (from the
ESP32 over the serial channel to your laptop console window).

## Solution Requirements
- Your solution should be implemented as a periodic cycling evaluation
  of the sensors (e.g., every 2s) followed by reporting of current
  values and setting of the output LEDs.
- You must use a hardware interrupt for the button press


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Complete self-assessment rubric

## References

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| 1. Reports time to console along with sensor readings  |  |  1     | 
| 2. Measures input from photocell |  |  1     | 
| 3. Measures and reports temperature in Engineering units  |  |  1     | 
| 4. Cyclic behavior at design frequency  |  |  1     | 
| 5. Uses hardware interrupt for button press   |  |  1     | 
| 6. Lights up correct LEDs on alarms    |  |  1     | 

