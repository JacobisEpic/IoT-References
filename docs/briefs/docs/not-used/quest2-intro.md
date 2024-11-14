# Sensor Central Introduction

Quest 2 is about collecting data from multiple sensors and displaying
them on a host. The challenges here are to make the individual sensors
work and then to get them all to work together. Things for you to
think about are:

- Different timing on each sensor -- how are these interleaved? Are they all synchronous?
- Does the timing control of each sensor work when the other sensors are running?
- Can the sensors capture data concurrently? Or do they need to be serialized?
- How fast can the data be captured and conveyed to the host?
- What pins should we use to allow physical interconnection to all of the devices at the same time and including 
reporting to a host over the UART and any diagnostics (e.g., using the LED display)
- How can we capture the data at the host to support consumption by a display program?

In-class exercises
1. Provide a flowchart of how you propose to program the ESP32 for the quest (on the whiteboard please)
2. Identify which pins will be used for what in your solution (make a table). Don't forget to incldue the console (whiteboard)
3. Investigate each sensor and design a data payload for communicating all of the measured data to the host. This could be raw or 
converted to engineering units (m) 
4. Report your results to your Quest 2 repo. Be prepared to discuss

<p align="center">
<img src="/images/quest2-new.png" width="100%">
</p>
<p align="center">
<i></i>
</p>
