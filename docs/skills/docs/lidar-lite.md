# Bringing up the LIDAR

Each kit has at least one LIDAR-Lite device. We have a mix of v1 and
v3 models (the current version is a V3). This device is a laser-based
ranging system that is relatively expensive ($120) when compared to
the rest of your kit's sensors and can *sometimes* be the most
accurate of the sensors in the kit.  Please search for the data sheet
and product guide based on the version you have.

*** v1 has a silver sticker, v3 has a white sticker, the v4 looks
    different -- rectangular***

***You may have and new ribbon cable on your device -- if so, note
   that the red wire does not correspond to Vin -- check the data
   sheet.***

<p align="center">
<img src="/docs/images/lidar-lite.jpg" width="50%">
</p>
<p align="center">
<i> LIDAR Lite (from Sparkfun)</i>
</p>

Here is a summary of key info on this device:
- Input voltage: 5V, max 100mA (NOTE: the newer v4 uses 3.3V)
- Interface: 3.3V logic
- I2C (**v3 uses fast-mode -- 400 kHz)**:
      - 7-bit slave address with a default value of 0x62
      - Some challenge if using two devices on same bus
    	 - Change default address value (reverts to default on power cycle)
    	 - Use the enable pin (22ms setup time)
- Range 40m, +/- 2.5cm

Interfacing:
- Wire up power (1), ground (6), I2C SCL (4), I2C SDA (5)
- Write to register 0x00 with value 0x04 (initiates and begins acquisition)
- **v1**: Poll the device until ACK received (sends NACK when busy) OR wait 20ms and then read high and low bytes
- **v3**: Repeatedly read register 0x01 until bit 0 (LSB) goes low
- Register 0x0F is upper byte of distance in cm; 0x10 is lower byte
- Single or multi-byte read possible; use register 0x8f for multi-byte read
- Alternatively, one could measure PWM pulse width -- see datasheet

There are code examples for the Arduino available. You will need to
adapt to ESP32 C but the examples for I2C can be readily adapted.

## Assignment
1. Wire up the LIDAR per the the specs.
2. Program the ESP32 I2C to initialize and read from the LIDAR continuously
3. Display results on the console
4. Evaluate the performance of the sensor and decide if this will be used on your crawler.
5. Write up results, pics, and the usual


## FAQ
1. The reads from the LIDAR are not working...
Answer:
The LIDAR lite doesn't support repeated starts.
- This means that you
cannot combine master reading and writing in one payload. So for your
read function, you should split the part that designates the read
register and the actual read into two separate I2C commands.
- Need to formally end (stop) your I2C command between each command. 
On every poll, you'll need to:
    	 - write 0x04 to register 0x00
    	 - Poll the Lidar-lite or wait 20ms
    	 - Read data
- The first byte is MSB, the second byte is LSB if reading two bytes at a time
- Don't forget to write an acknowledgement to the slave from the ESP -- ACK_VAL
- Consult the data sheet for more information: http://static.garmin.com/pumac/LIDAR_Lite_v3_Operation_Manual_and_Technical_Specifications.pdf
2. How do I run two LIDARs on the same I2C bus?
Answer: see the [recipe for changing LIDARlite V3 I2C addresses](/docs/briefs/recipes/docs/recipe-lidarlite.md)


## Reference material
- [LIDAR-Lite Arduino Sketch](https://www.robotshop.com/community/blog/show/lidar-lite-laser-rangefinder-simple-arduino-sketch-of-a-180-degree-radar)
- [LIDAR-Lite V1/V2 docs](https://github.com/PulsedLight3D)
- [LIDAR-Lite V3 Datasheet](http://static.garmin.com/pumac/LIDAR_Lite_v3_Operation_Manual_and_Technical_Specifications.pdf)
- [Recipe for changing LIDARlite V3 I2C addresses](/docs/recipes/docs/lidarlite.md)
