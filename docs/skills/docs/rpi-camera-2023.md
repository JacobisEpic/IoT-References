# Web Camera on the Pi Zero (UPDATED with recipe 2023-03-17)

We are using the Pi Zero to support video sourcing and streaming. The
camera comes from Adafruit as product no. 3170 (Camera Board v2).
This camera can be used in lots of available software and
applications. We are recommending specific installs, but you are
welcome to get more exotic with different configurations and camera
features.

This is a basic approach as a
[webcam](https://www.hackster.io/narender-singh/portable-video-streaming-camera-with-raspberry-pi-zero-w-dc22fd)
using the motion software.  Here is another useful tutorial
[webcam_tutorial](https://pimylifeup.com/raspberry-pi-webcam-server/),
depending on your dependencies/version, a few of you may also need to
also run "sudo
LD_PRELOAD=/usr/lib/arm-linux-gnueabihf/libv4l/v4l1compat.so motion
-n"

Raspbian (now Raspberry Pi OS) also supports camera still and video
options as described
[here](https://www.raspberrypi.org/documentation/raspbian/applications/camera.md)
and setup
[here](https://www.raspberrypi.org/documentation/configuration/camera.md).

Here is another approach as a [time-lapse
camera](https://learn.adafruit.com/raspberry-pi-wearable-time-lapse-camera/software)
that illustrates some of the camera configuration options.

## Recipe
After banging our heads agaist the solutions above, we put together a
[recipe for bringing up the pi-cam](/docs/briefs/recipes/recipe-picam2.md) using `motion`. It is perhaps a
little fragile based on package updates but seems to work as of
2023-03-17. 


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
