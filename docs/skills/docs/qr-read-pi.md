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
- socket

Then you program the pi using python with the following strategy:

1. Use picamera2, python image library (PIL Fork), zbarlight
2. Configure and start picam2
3. While no QR detected
   a. Read camera frame from picam2
   b. Test for QR code, save image as qr.jpg
5. Open image and decode QR
6. Send decoded value to node server via socket/datagram

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

