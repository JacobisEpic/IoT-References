# Carmin 
This quest is to build an instance of a wearable device that records biometrics and reports back to a central graphical hub.

<p align="center">
<img src="/docs/images/carmin1.jpg" width="40%">
</p>
<p align="center">
<i>Smart Watch</i>
</p>

The key features of the wearable are going to be:
- Keeps track of time of day (HR:MIN)
- Provides start and stop of recording of activity
- Provides an alert (e.g., alarm/buzzer) when reach temperature threshold
- Measures number of steps during activity, per interval (such as 1 hour or 1 day)
- Measures body temperature, captures during activity
- Reports data to laptop for display as stripchart in real time (steps, temperature)

Later, in the next quest, we will collect data from multiple Carmins
over wireless links, but the basic sensing and timer activities will
be developed here.

<p align="center">
<img src="/docs/images/carmin2.jpg" width="80%">
</p>
<p align="center">
<i>Smart Watch Elements</i>
</p>

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions



## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Displays clock time on alpha display as HR:MIN |  |  1     | 
| Functions as a simple activity timer (start, stop, reset) |  |  1     | |
| Provides continuous reporting of steps per 10s interval to laptop |  |  1     | 
| Provides continuous reporting of body temperature per 10s interval to laptop |  |  1     | 
| Data at laptop plotted as stripcharts |  |  1     | 
| Provides alert function with buzzer on alarm |  |  1     | 


## Reference material
- [Serial Port Module](https://www.npmjs.com/package/serialport)
- [Serial to Node Without a File Example](https://github.com/BU-EC444/04-Code-Examples/tree/main/serial-esp-to-node-serialport)