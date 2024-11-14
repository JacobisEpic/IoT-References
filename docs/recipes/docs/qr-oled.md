### Display QR on the OLED recipe

This recipe assumes that the OLED is connected to the ESP32 and you
have successfuly run the OLED display to display text using the sample
code. The strategy here is to have a set of pre-defined QR codes that
are stored on the ESP32 versus being generated there.  In this recipe
the QR codes are generated offline and hard-coded into the firmware.

## Recipe
1. Generate a QR code (e.g., we encoded a text “0A”) at 200x200 resolution using a free online site.
2. Convert the QR code to an array of bytes. We used [this one](https://mischianti.org/images-to-byte-array-online-converter-cpp-arduino/)
3. Select your saved QR code as input to the converter. Settings:
    - Canvas size: 128x64
    - Scale to fit, keeping proportions
    - Center horizontally
    - Output format: plain bytes
    - Preview in the tool
4. Add the byte array to your code as a data structure
5. It’s ready to send to the display

<p align="center">
<img src="/docs/images/oled.jpg" width="50%">
</p>
<p align="center">
<i>OLED Display Unit Showing QR Code "0A"</i>
</p>


## References
- [Images to Byte Array](https://mischianti.org/images-to-byte-array-online-converter-cpp-arduino/)
- [Sample code for OLED bitmap graphics display](https://github.com/BU-EC444/04-Code-Examples/tree/main/oled-qr-display)


