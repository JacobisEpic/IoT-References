# Setup Espressif Toolchain

We are using the Huzzah32 feather board sold by Adafruit based on the ESP32
part from Espressif. We selected this board due to the number of
features supported including BLE and WiFi, the ability to program in
C, access to a RTOS, and its low cost (about $18 each in
quantities of 100).  There is some Arduino code that goes with the
board, but we will focus on working with the board in C.  This step
installs the drivers and code associated with the board including the
toolchain for getting your code cross-compiled and downloaded to your
board as firmware.

<p align="center">
<img src="/docs/images/ESP32.jpg" width="25%">
</p>
<p align="center">
<i>Huzzah32 Feather -- ESP32</i>
</p>

## Assignment
<!-- 1. Install USB driver from [Adafruit](https://learn.adafruit.com/adafruit-huzzah32-esp32-feather/using-with-arduino-ide), which points you to [Silabs](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) -->

2. Follow the steps on [Espressif Getting Started Guide](https://esp-idf.readthedocs.io/en/latest/get-started/index.html) consisting generally of:
   - Install prerequisites
   - Get ESP-IDF from Github (or install your preferred IDE along with the IDF)
   - Set up the tools -- the tools installation path is tricky
   - Set up the environment variables
3. Using the example code in `esp-idf/examples/get-started,` flash an ESP32 board to blink the onboard LED
   - Hint: check out the pinout and pin mapping in the [Utilites](/docs/utilities/README.md) tab
4. Summarize results with a screenshot in your README.md for the skill in your local copy. 
Then commit and push to the appropriate folder of your github account.

## Reference material
- [Getting Started Guide](https://esp-idf.readthedocs.io/en/latest/get-started/index.html)
- [Setting up a New Project](/docs/design-patterns/docs/dp-project.md)
- [Sample project](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#example-project)
- [Install USB driver](https://learn.adafruit.com/adafruit-huzzah32-esp32-feather/using-with-arduino-ide)

## Notes for Mac users
- No spaces are allowed in directory or file names for the ESP toolchain
- Get Xcode – from the Apple App store, this takes a while.
- Create a .profile in root with this as its contents to automate environment variables setup:

```
. $HOME/Desktop/esp/esp-idf/export.sh
```
- Port numbers are indicated by `/dev/cu.usbserial-XXXX` The `XXXX` number is unique to the ESP32 board and you will need to identify and use this number when you attach different ESP32 devices.



## Notes for Windows users
- Python version -- technically supports older Python versions but some of the install scripts rely on Python 3.7 commands, so you should:
  - Either use Python version 3.7 (let the installer install it automatically)
  - Or edit the install scripts to remove `capture_output` in the `subprocess.run` commands
- Keep your directories in check, i.e. know where you installed everything


## Other Install Notes
- (Saying it again:) No spaces in paths please
- The Blink README provides instructions on how to use menuconfig and monitor
- For Blink to work, you need to set the GPIO pin to 13 for the on-board LED. Do this using menuconfig
- The ESP32 pinout maps to the featherboard pins. See the Utilities tab for these pinouts
- You probably want your code located both in the path of your build tools, your IDE, and your git files. Think about how to do this.









<!-- ```
#esp-idf stuff -- this is a comment
export PATH=~/Desktop/ec444/esp/xtensa-esp32-elf/bin:$PATH
export IDF_PATH=~/Desktop/ec444/esp/esp-idf
```-->
