# Bringing up the LIDAR

This page refers to the Garmin v4 LIDAR.

Each kit has at least one LIDAR-Lite device. This device is a
laser-based ranging system that is relatively expensive (this one is $60) when
compared to the rest of your kit's sensors and can *sometimes* be the
most accurate of the sensors in the kit.  Please search for the data
sheet and product guide based on the version you have.

***This model v4 uses Vin of 5V, but the I2C lines use 3.3V. Be careful with wiring***.

<p align="center">
<img src="/docs/images/v4-closeup2.jpg" width="30%">
</p>
<p align="center">
<i> Garmin LIDAR v4 with Ribbon</i>
</p>

<p align="center">
<img src="/docs/images/garmin-wires.jpg" width="30%">
</p>
<p align="center">
<i> Garmin LIDAR v4 with Female to Male Jumpers</i>
</p>

Here is a summary of key info on this device:
- Input voltage (Vin): 5V, max 85mA 
- Interface: 3.3V logic
- I2C:  supports fast mode 
- 7-bit slave address with a default value of 0x62 (but changeable in software); 8 bit modes available
- Range 5cm to 10m 40m, +/- 5cm at 10m

Interfacing:
- Wire up power (1), ground (2), I2C SDA (3), I2C SCL (4)
- 22ms delay for boot up
- Write to register 0x00 with value 0x04 (initiates and begins acquisition)
- Read register 0x01
- Repeat read of 0x01 until bit 0 (LSB) goes low
- Read two bytes from 0x10 (low byte 0x10 then high byte 0x11) to get 16-bit distance in cm

<p align="center">
<img src="/docs/images/v4-top-pinout.jpg" width="25%">
</p>
<p align="center">
<i> Garmin LIDAR v4 Pinout (Top View)</i>
</p>



There are code examples for the Arduino available. You will need to adapt to ESP32 C but the examples for I2C can be readily adapted.

***Note:*** interfacing to the thin ribbon wire will be challenging. You will need to strip the wires and make connections somehow. We do not have
a good solution here. Figure it out. 

## Assignment
1. Wire up the LIDAR per the the specs.
2. Program the ESP32 I2C to initialize and read from the LIDAR continuously
3. Display results on the console
4. Evaluate the performance of the sensor -- range vs. actual (tape measure)
5. Write up results, pics, and the usual


## Reference material
- [Garmin Lidar v4](http://static.garmin.com/pumac/LIDAR-Lite%20LED%20v4%20Instructions_EN-US.pdf)
- [Garmin Arduino Examples](https://github.com/garmin/LIDARLite_Arduino_Library)
