# Occupancy Counting

<p align="center">
<img src="/docs/images/occ.png" width="100%" />
</p>

<p align="center">
Ocupancy Sensing
</p>

People counting ("occupancy counting") is an important objective in
many smart space use cases. Example use cases include: a fire brigade
wanting to know if a room is cleared of people (0 people present); a
diner wants to know if there are seats available in a coffee shop (> 1
seat with no occupant); or a control system can adjust airflow based
on the number of people in a room (minimum estimated count with P=1).


## Description

Your goal in this quest is to "bring up" many of the sensors in the kit
in order to sense occupancy. Results will be displayed in engineering units on 
the console and displayed 
using a graphics package and GUI. The sensors in question are:
- Thermistor: if hot, then a person is sitting on a chair or touching the sensor; cold: empty
- Solar cell: if dark, then the room is empty; if light, the lights are on and someone is present
- Ultrasonic 1: if range drops briefly, someone has passed through a space
- IR Rangefinder: if the range changes, someone has into our out of a volume

<p align="center">
<img src="/docs/images/occ-sol.png" width="100%" />
</p>
<p align="center">
Occupancy Sensor Set
</p>

By "bring up" this means:
- Read the spec sheets on voltage and power requirements for each sensor and make a list of what you need from the ESP
  (note voltage ranges and whether a voltage divider is required)
- Sort out which I/O or ADC channels you plan to use for each sensor
- Wire up each sensor on the breadboard (do this iteratively, not all at once for least frustration)
- Write and/or adopt code from ESP distribution to read each sensor and validate the input values
- Convert raw values to engineering units
- Display on your console

Once you have successfully dumped the measured values on the console,
the next step is to deliver them to a graphing program.

Conveniently, the sensors included all output measurements as an
analog signal. Later you will investigate other digital ways to
interface to sensors. These sensors will be used to support different
quests so it's good to have a modular solution. 

## Solution Approach
This problem breaks down into different independent parts. We
recommend that you use this breakdown so that you can independently
test and validate each before you integrate:

1. Module to display values on the console as text
2. Module to read the ultrasonic sensor
3. Module to read the thermistor
4. Module to read the solar cell
5. Module to read the IR sensor
6. Module to save console data to a file on your host in text or JSON
7. Module to read data from your host file and plot (we recommend using CanvasJS and node.js on your laptop)
8. Module to blink LEDs when you decide that occupancy is detected (good for debugging too)

More notes: Your ESP software solution can be designed in different ways. This is a cyclic instrumentation problem
  (a) In each cycle, read each sensor, then report to the console, or
  (b) In each cycle, start n independent tasks, each reading a sensor and saving results; a task writes data to the console

## Solution Requirements
- For each sensor you integrate, establish the ranges, offsets, and limitations
- Specify the pin assignments (table) for the ESP and each device
- Develop formulae to convert measured units into common engineering units among the sensors
- Plotting: your plotting part should generate real-time strip-chart display(s)
- You must have at least one LED that will indicate the presence of a detection of occupancy for the duration of the detection

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Complete self-assessment rubric
5. Investigative question: How fast can you sample each sensor and at what resolution based on the data sheet specs for each item?


## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Periodic reporting of ultrasonic range in m |  |  1     | 
| Periodic reporting of IR range in m |  |  1     | 
| Periodic reporting of temperature in C |  |  1     | 
| Periodic reporting of solar output in V |  |  1     | 
| Results displayed at host as text |  |  1     | 
| Results graphed at host continuously based on reporting period |  |  1     | 
| Ocupancy indicator is functional |  |  1     | 
| Demo delivered at scheduled time and report submitted in team folder with all required components |  |  1     | 
