# OLED Dislay

We acquired the OLED display specifically for showing bitmaps of QR
codes for near field communication using a camera. It's an I2C device
which is handy for ease of wiring.  This skill guides you through
setting up this device.

<p align="center">
<img src="/docs/images/oled-1306.jpg" width="25%">
</p>
<p align="center">
<i>OLED Display Unit</i>
</p>


## Wiring
- ESP32 SDA -- OLED Data
- ESP32 SCL -- OLED Clk
- ESP32 pin 33 -- OLED Rst
- ESP USB -- OLED VIN
- ESP GND -- OLED GND

<p align="center">
<img src="/docs/images/oled.jpg" width="50%">
</p>
<p align="center">
<i>OLED Display Unit Wiring to ESP32</i>
</p>


## Assignment/Requirements

1. Wire up the OLED display with the I2C bus
2. Using the sample code (two versions below), create a function to display
   - Demonstrate a function to display a string without scrolling
   - Demonstrate adding a graphic: a QR code of your choice
3. Demonstrate your results, writeup and report with a picture and any other evidence

## Reference material
- [Sample code for OLED text display](https://github.com/BU-EC444/04-Code-Examples/tree/main/oled-txt-display)
- [Sample code for OLED bitmap graphics display](https://github.com/BU-EC444/04-Code-Examples/tree/main/oled-qr-display)

