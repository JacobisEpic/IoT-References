# Sensor Central

Your goal in this quest is to bring up most of the analog sensors in the kit and display the measured values on a GUI.

## Skill Cluster:

- [Battery Monitor](/skills/battery-monitor)
- [Thermistor](/skills/thermistor)
- [Ultrasonic 1](/skills/ultrasonic1)
- [IR Rangefinder](/skills/ir)
- [Node.js](/skills/node-js)
- [CanvasJS or other graphing program](/skills/canvasjs)
- [Raspberry Pi](/skills/rpi)

## Description

<p align="center">
<img src="/docs/images/quest2-new.png" width="100%" />
</p>
<p align="center">
<i> Sensor Central</i>
</p>

By "bring up" this means:
- Read the spec sheets on voltage and power requirements for each sensor and make a list of what you need from the ESP
  - note voltage ranges and whether a voltage divider is required
- Sort out which I/O or ADC channels you plan to use for each sensor
- Wire up each sensor on the breadboard (do this iteratively, not all at once for least frustration)
- Write and/or adopt code from ESP distribution to read each sensor and validate the input values
- Convert raw values to engineering units
- Display on your console

Once you have successfully dumped the measured values on the screen,
the next step is to deliver them to a plotting program.

Conveniently, the sensors included all output measurements as an analog signal. Later you will investigate other digital ways to interface to sensors. These sensors will be used to support different quests so it's good to have a modular solution. For each sensor/modality, plan to collect data and compare
results as graphic output. To make this work you will need to
adopt a way to bring the measured data from the ESP32 to a connected
host where you need to plot the collected data.

This problem breaks down into different independent parts. We
recommend that you use this breakdown so that you can independently
test and validate each before you integrate:

1. Module to display values on the console as text
2. Module to read the ultrasonic sensor
3. Module to read the thermistor
4. Module to read the battery (voltage divider)
5. Module to read the IR sensor
6. Module to save console data to a file on your host in text or JSON
7. Module to read data from your host file and plot (we recommend using CanvasJS and node.js on your laptop)

More notes: Your ESP program can be designed different ways. This is a cyclic instrumentation problem
  (a) In each cycle, read each sensor, then report to the console, or
  (b) In each cycle, start n independent tasks, each reading a sensor and saving results; a task writes data to the console

## Solution Requirements
- For each sensor you integrate, establish the ranges, offsets, and limitations
- Specify the pin assignments (table) for the ESP and each device
- Develop formulae to convert measured units into common engineering units among the sensors
- Plotting: your plotting part should generate real-time strip-chart display(s)

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: How fast can you sample each sensor and at what resolution based on the data sheet specs for each item?

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Does A  |  |  1     | |
| Does B  |  |  1     | |
| Does C  |  |  1     | |
| Does D  |  |  1     | |
| Does E  |  |  1     | |
| Does F  |  |  1     | |
| Does G  |  |  1     | |
