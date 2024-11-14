# Ultrasonic Range Sensor

Another common sensor uses ultrasonic signals (meaning, a frequency
above human hearing; had to look it up). The ones we use are for
'ranging' -- estimating the distance from the sensor to an object that
reflects the sound. The sensor times how long a signal pulse takes for
an echo to return, and based on a value for the speed of sound,
calculates range. Like most of the sensors, it has minimum and maximum
operating ranges. Best to look up the sensor part number to understand
where a particular sensor works best. We have some variation in part
numbers for the set distributed to the kits.

Ranging sensors (ultrasonic or otherwise) can also be used for spatial
mapping by scanning a value with repetitive samples and then
interpreting the 'point cloud' of returned results. This is more often
done with lasers, but the technique can be applied to any ranging
sensor.

Lastly, there is an algorithm called Simultaneous Localization and
Navigation (SLAM) that attempts to use the aforementioned data to both
map the space and use the map for navigation. Handy for autonomous
vehicles.

<p align="center">
<img src="/docs/images/Ultrasonic1.jpg" width="50%">
</p>
<p align="center">
<i> Sparkfun Ultrasonic Range Finder</i>
</p>

Notes on thethe Sparkfun sensor
- This device is designed for 5V but appears to accept Vcc of 3.3V
- As per the data sheet, you send the device a pulse and time the response.
- Distance reported as a function of the time delay

We recommend (updated)
- Use [RMT (Remote Control) in IDF](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/rmt.html)
- 10us pulse with RMT TX
- Measure pulse with RMT RX
- Measuring the duration of the return pulse
- Convert to cm
- Pinout:
	- TX - pin 25 -- trigger
  	- RX - pin 26 -- echo


## Assignment
1. Look up the specs of the ultrasonic sensor and design an appropriate way to connect to the ESP32 (PWM)
2. Wire it up
3. Write the code to read from the device, convert to engineering units, and display the results on the console, sampled every 2 s.
4. Write up results, pics, and the usual


## Reference material
- [Sparkfun Ultrasonic Range Finder](https://www.sparkfun.com/products/13959)
- [Range Finder Data Sheet](https://cdn.sparkfun.com/assets/b/3/0/b/a/DGCH-RED_datasheet.pdf)
