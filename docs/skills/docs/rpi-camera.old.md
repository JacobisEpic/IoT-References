# Web Camera on the Pi Zero
(UPDATED due to changes in Pi OS bookworm 2023-10-17)

We are using the Pi Zero to support video sourcing and streaming. The
camera comes from Adafruit as product no. 3170 (Raspberry Pi Camera
v2.1 on the silkscreen).  This camera can be used in lots of available
software and applications. We are recommending specific
installs. Straying to other software is fine but expect some effort to
make them work.

Raspbian (now Raspberry Pi OS) also supports camera still and video
options as described
here [Raspberry Pi OS Camera
Software](https://www.raspberrypi.com/documentation/computers/camera_software.html).

## Recipe

After banging our heads agaist the solutions above (again now due to
changes in Pi OS), we put together a [recipe for bringing up the
pi-cam](/docs/recipes/docs/video.md).  2023-10-25.


<p align="center">
<img src="/docs/images/adafruit-pi-cam.jpg" width="30%">
</p>
<p align="center">
<i>RPi Zero with Camera V2 (Image from Adafruit)</i>
</p>

## Assignment
1. Install the basic webcam software (different options avove, or others). 
2. Demonstrate video streaming delivered to a computer browser on a network address on your subnet
3. Alternatively, you can show video streamed into a browser running on the RPi. 
4. Report.

## Reference Material
- [Raspberry Pi Camera V2](https://www.raspberrypi.org/products/camera-module-v2/)
- [Raspbery Pi Camera Module Applications](https://www.raspberrypi.org/documentation/raspbian/applications/camera.md)
- [Pi OS Configuration](https://www.raspberrypi.org/documentation/configuration/camera.md)
- [webcam](https://www.hackster.io/narender-singh/portable-video-streaming-camera-with-raspberry-pi-zero-w-dc22fd)
- [webcam_tutorial](https://pimylifeup.com/raspberry-pi-webcam-server/)
- [time-lapse camera](https://learn.adafruit.com/raspberry-pi-wearable-time-lapse-camera/software)


