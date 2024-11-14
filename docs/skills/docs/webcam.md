# Using the USB Webcam on the Raspberry Pi Zero

The RPi and linux supports using an off-the-shelf webcam. We have
Logitech webcams that work well and are handy for adding FPV to any
car-crawler-robot-racing-type project.  This is mostly a software
exercise.

Note that your goal here is to have a webcam that you can access from
across the network in real-time. There are many other applications,
such as capturing stills and performing video analysis (e.g., using
OpenCV), but we are not interested in these techniques at the moment.

<p align="center">
<img src="/docs/images/USBCam.jpg" width="50%">
</p>
<p align="center">
<i>Logitech Webcam</i>


## Assignment
1. Set up your RPi (separate skill)
2. Investigate options for setting up a webcam on the Rpi. Remember,
your goal is to have a reliable A/V source that can be transmitted
wirelessly to a web client. We recommend Motion ([Installation guide
here](https://pimylifeup.com/raspberry-pi-webcam-server/))
3. Install your webcam software.
4. Set up and demonstrate your webcam operating from a web browser on a different machine.
5. The usual pix and writeup

## Reference material
- [Raspbian/fswebcam](https://www.raspberrypi.org/documentation/usage/webcams/)
- [Baby Monitor](https://www.raspberrypi.org/forums/viewtopic.php?p=457887#p457887)
- [Web Server Cam](https://pimylifeup.com/raspberry-pi-webcam-server/)
- [Another Web Server Cam](https://www.instructables.com/id/How-to-Make-Raspberry-Pi-Webcam-Server-and-Stream-/)
-  mjpg-streamer -- [known to work as of Nov-2019]
  - [Tutorial](https://wouterdeschuyter.be/blog/how-to-create-a-15-dollar-web-controllable-camera-with-a-raspberry-pi-zero)
  - [Source](https://github.com/jacksonliam/mjpg-streamer)
