# Ultrasonic Range Sensor

A common sensor uses ultrasonic signals (meaning, a frequency
above human hearing). The ones we use are for
***'ranging'*** -- estimating the distance from the sensor to an object that
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
<img src="/docs/images/Ultrasonic2.jpg" width="25%">
</p>
<p align="center">
<i> Ultrasonic Range Finder -- Maxbotics</i>
</p>

Notes on the Maxbotics Sensor
- Accepts Vcc of 3.3V to 5.5V, but we want you to use 3.3V from ESP if possible
- Has different ways to connect:
  - PW output with measurement of 300us to 5,000us (1us/mm) -- basicallt you measure the pulse width
  - Analog output (Vcc/1024)/5mm -- altnernative to measure analog voltage ith ADC
  - Serial (most accurate): sends ASCII 'R' followed by 4 ASCII range characters -- use UART to interface
- Continuously ranges if pin 4 left open (updated every 100ms)
- Sensitive to voltage supply changes, use capacitor on Vcc if you have one

We recommend:
- UART for best accuracy
- ADC for simplicity and use of pins

<p align="center">
<img src="/docs/images/maxbotics-pinout.jpg" width="40%">
</p>
<p align="center">
<i> Pinout Enlarged</i>
</p>

## Assignment
1. Look up the specs of the ultrasonic sensor (multiple depending on your part number -- different range capability) 
and design an appropriate way to connect to the ESP32 (UART, ADC, PWM)
2. Wire it up
3. Write the code to read from the device, convert to engineering units, and display the results on the console, sampled every 2 s.
4. Write up results, pics, and the usual


## Reference Material
- [Ultrasound](https://en.wikipedia.org/wiki/Ultrasound)
- [SLAM](https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping)
- [Maxbotics Range Finder Specs](https://www.maxbotix.com/documents/HRLV-MaxSonar-EZ_Datasheet.pdf)

<p align="center">
<img src="/docs/images/maxbotics.png" width="70%">
</p>
<p align="center">
<i> Wiring</i>
</p>

