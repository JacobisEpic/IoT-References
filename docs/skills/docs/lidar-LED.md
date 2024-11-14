# Bringing up the LIDAR

The kit includes a device from Sparkfun called the TFMini. It's not
actually a LIDAR (does not use a laser) but it serves the same
function with an IR LED-based time of flight (TOF) function.

It's a serial device so you will need to fiddle with the UART to make
this sensor work. It's a $40 part, one of the more expensive parts in
kit. No cooking please.

And with respect to drivers, Sparkfun includes reference designs in
Arduino code which you are welcome to adapt for the ESP32 code in C.
As before, the ESP-IDF distro includes examples for configuring and
using the UART.

<p align="center">
<img src="/docs/images/lidar-LED.jpg" width="50%">
</p>
<p align="center">
<i> TFMini "LIDAR"</i>
</p>

Wiring/specs
- Green: UART_TX (3.3V)
- White: UART_RX (3.3V)
- Red: +5V
- Black: GND
- Baud rate: 115200, 8 bits, 1 stop, 0 parity)
- Range: 30 cm -- 12 m
- High peak current of 800mA -- this may give us trouble, we will find out as we go


Data from device:
- Hex output, 9 byte frame
- Frame
  - 0x59 header 1
  - 0x59 header 2
  - Distance, lower byte
  - Distance, higher byte
  - Strength, lower byte
  - Strength, higher byte
  - Reserved
  - Signal quality
  - Checksum

We recommend:
- Don't mess with the arduino libraries. Go straight to the data sheet to understand the serial data
- It appears that this device just runs continuously. Your serial read algorithn will need to align on the headers before interpreting the data as range
- Most of your code will need to deal with corrupt data, flushing data until you are aligned.
- Not required to use checksum, but might improve confidence on transmitted data
- The ESP32 has 3 UARTs.  This example shows using UART 1 to communicate with a device separate from the USB/console connection. 
[UART Echo](https://github.com/espressif/esp-idf/tree/758db1e00/examples/peripherals/uart/uart_echo).
 

## Assignment
1. Wire up the LIDAR per the the specs.
2. Program the ESP32 UART to read from the LIDAR
3. What is the max sampling rate of this device?
4. Show data output from this device on your console in engineering units (not just hex please)
4. Write up results, pics, and the usual



## Reference material
- [Sparkfun TFMini](https://www.sparkfun.com/products/14588)
- [TFMini Data Sheet 1](https://cdn.sparkfun.com/assets/5/e/4/7/b/benewake-tfmini-datasheet.pdf)
- [TFMini Data Sheet 2](https://cdn-shop.adafruit.com/product-files/3978/3978_manual_SJ-PM-TFmini-T-01_A03ProductManual_EN.pdf)
- [ESP-IDF UART API Reference](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/uart.html)
- [ESP-IDF Code example in distro](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/uart)

<p align="center">
<img src="/docs/images/LIDAR-wiring.jpg" width="50%">
</p>
<p align="center">
<i> Lidar-LED Range Finder</i>
</p>