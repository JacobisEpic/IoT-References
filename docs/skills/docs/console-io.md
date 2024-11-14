# Console I/O

In this exercise, you will explore the different ways to communicate
between your PC and the ESP32 over the wired USB interface.

<p align="center">
<img src="/docs/images/terms.jpg" width="80%">
</p>
<p align="center">
<i>Components Involved in Delivering Serial Data from ESP32 to Laptop Terminal (Console)</i>
</p>

We've included a bunch of ways to interact with the console in the
[Console I/O Design Patterm](/docs/design-patterns/docs/dp-console.md) and you may
find other ways on the ESP-IDF documents. The starting point is to get
UART to work and get one or two characters. When in doubt, consult the
ESP-IDF documents.

In addition, we've tossed in some quirks to jog your memory when it
comes to programming basics. Namely, you might need to use a switch
statement, convert data types or number types, and remember what a
character array is. This assignment may seem tedious but good skills
here will take you far.

## Assignment
1. Review the [Console I/O Design Patterm](/docs/design-patterns/docs/dp-console.md)
2. Bring up the Echo program example. This example demonstrates a keystroke
being sent to the ESP32 and the ESP32 'echoing' the character back to the console program. ***Note you will need to use Menuconfig to change the UART to 0, the TX pin to 1, and the RX pin to 3.***
3. Write and demonstrate a new program that performs the following (dealing with multiple characters sent to and from the ESP32):
  - Has three modes, switch between the modes with key input 's'
  - Mode 1: Toggle the onboard LED based on key input 't'
  - Mode 2: Echo input (2 or more characters) from the keyboard to the console
  - Mode 3: Echo a decimal number input as a hexadecimal
4. Take photos and write up a description in README.md and upload to github.

<p align="center">
<img src="/docs/images/console-io.png" width="80%">
</p>
<p align="center">
<i>Example console output</i>
</p>


## Reference material
- [Console IO Brief](/docs/design-patterns/docs/dp-console.md)
- [ESP32 Echo Example](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/uart/uart_echo)
- [ESP-IDF Programming Guide: UART](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/uart.html)
- [Standard I/O Stream](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/storage/vfs.html#standard-io-streams-stdin-stdout-stderr)
