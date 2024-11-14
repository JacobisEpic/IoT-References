# Swiss-Army Tape Measure

A Swiss Army knife is a multi-tool that in addition to providing a
knife, provides lots of other tools and gadgets.  Our "Swiss Army"
Tape Measure is intended to exercise many of the measurements devices
available in the class kit. Your job is to bring this set to
life, providing data collection on the variety of sensing devices and
plotting the captured data in a useful way.  Conveniently, the sensors
included all measure some form of distance or range. These will be useful later
in supporting self-driving, navigation, and positioning.

For each sensor/modality, plan to collect data and compare results in
a single graphic output. To make this work you will need to adopt a
way to bring the measured data from the ESP32 to a display console
where you need to plot the collected data.  

<p align="center">
<img src="/docs/images/quest2.png" width="100%" />
</p>
<p align="center">
<i> Swiss Army Tape Measure</i>
</p>

This problem breaks down into different independent parts. We
recommend that you use this breakdown so that you can independently
test and validate each before you integrate:

1. Module to display values on the console
2. Module to read the ultrasonic sensor
3. Module to read the lidar 
4. Module to IR sensor
5. Module to read the wheel speed sensor
6. Module to save console data to a file on your host in text or JSON (laptop)
7. Module to read data from your host file and plot (we recommend using ~~charts.js~~ CanvasJS and node.js on your laptop)

NOTE: Reading the wheel sensor can be a separate demo (does not need to be integrated as it requires battery on USB port)

## Assignment
1. List the sensors that you will integrate and establish the ranges, offsets, and limitations of each sensor
2. Develop formulae to convert measured units into common engineering units among the sensors
3. Write a program to service each sensor at regular intervals to produce a real-time strip-chart display function.
4. Transfer data to a host computer for plotting either by
   - Direct to a plotting program (e.g., Matlab, or web app such as node.js and ~~charts.js~~ CanvasJS)
   - To a file, then a plotting program
5. Use the default assessment rubric to realize your implementation
6. Demonstrate your solution
7. Write up a description of how you built your solution. Include
concepts, modules, APIs, tools, etc.
8. Submit a < 90s video of your report. Everyone must be on the video.


<p align="center">
<img src="/docs/images/stripchart.png" width="100%" />
</p>
<p align="center">
<i> Example Stripchart from NOAA Weather Site</i>
</p>


## Reference material
- [Node.js](https://nodejs.org/en/) Node is a framework for hosting and running HTTP (web) sites
- [CanvasJS](https://canvasjs.com)


# Quest 2 In-Class

Quest 2 is about collating data from multiple sensors and displaying
them on a host. The key problem here is not specifically getting the
sensors to work, but in getting them all to work together. Things for
you to think about are:

- Different timing on each sensor -- how are these interleaved?
- Does the timing control of each sensor work when the other sensors are running?
- Can the sensors capture data concurrently? Or do they need to be serialized?
- How fast can the data be captured and conveyed to the host?
- What pins should we use to allow physical interconnection to all of the devices at the same time and including 
reporting to a host over the UART and any diagnostics (e.g., using the LED display)
- How can we capture the data at the host to support consumption by a display program?

In-Class assignment
1. Provide a flowchart of how you propose to program the ESP32 for the quest (on the whiteboard please)
2. Identify which pins will be used for what in your solution. Don't forget to incldue the console (whiteboard)
3. Investigate each sensor and design a data payload for communicating all of the measured data to the host. This could be raw or 
converted to engineering units (m) 
4. Report your results to your Quest 2 repo. Be prepared to discuss

<p align="center">
<img src="/docs/images/quest2.png" width="100%" />
</p>
<p align="center">
<i> </i>
</p>

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
