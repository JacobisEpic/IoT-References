# QR Reading with ESP32 and Pi

This assumes you are using the Pi Zero W (arm6, 32bit) and Adafruit
product no. 3170 (Camera Board v2).

## Recipe
You will need to bring up an ESP32 that displays a QR code:
- [Recipe for QR-OLED](/docs/recipes/docs/qr-oled.md)

Then you need to bring up the pi-camera to capture images
- [Recipe for bringing up the pi-cam](/docs/recipes/docs/video.md)

Relevant tools to be used in python on the pi include:
- Python
- PiCamera2
- Zbarlight
- PIL

Then you program the pi using python with the following strategy:

1. Use picamera2, python image library (PIL Fork), zbarlight
2. Create a stream
3. Read camera frames from pi-cam at 640x480 and 30f/s into stream
4. Sample latest frame from stream
5. Convert the sample image into grayscale
6. Read code from image using function scan_codes
7. If it exists, send decoded value to destination (node server or otherwise)
8. Flush stream and repeat

## Assignment
1. Build and demonstrate
2. Report 


## Reference Material
- [Recipe for QR-OLED](/docs/recipes/docs/qr-oled.md)
- [Recipe for bringing up the pi-cam](/docs/recipes/docs/video.md)
- [Raspberry Pi OS Camera](https://www.raspberrypi.com/documentation/computers/camera_software.html)
- [Picamera2](https://github.com/raspberrypi/picamera2)
- [Zbarlight](https://pypi.org/project/zbarlight/)
- [Pillow (PIL Fork)](https://pillow.readthedocs.io/en/stable/index.html)

