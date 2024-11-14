# Web Camera on the Pi Zero
(UPDATED 2024-10-10)

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

<p align="center">
<img src="/docs/images/adafruit-pi-cam.jpg" width="30%">
</p>
<p align="center">
<i>RPi Zero with Camera V2 (Image from Adafruit)</i>
</p>

## Assignment
1. Bring up your pi with the latest raspberri pi OS
2. Attach the pi camera (be careful of the small black strip of the ribbon connector)
3. Follow the instructions for the [RPi Camera Software](https://www.raspberrypi.com/documentation/computers/camera_software.html). On the headless pi (no monitor, do the following:
     - Test with `rpicam-hello`
     - Test with {many other application options}
4. Now demonstrate networking the video to another client
     - On the console (locally on the pi), or in ssh (remotely), run:
`libcamera-vid -t 0 --inline --listen -o tcp://192.168.1.211:3333`
     - This puts the video on the network at 192.168.1.211:3333 on my network
     - With a monitor attached it spawns a new window with video
     - Without a monitor in ssh it shows a text description of each frame set
5. Playing the video
     - With a monitor, you can run (in a console window) the vlc player (comes installed with Pi OS)
`vlc tcp/h264://192.168.1.211:3333` 
     - Without a monitor, you need to install the vlc player on your local laptop (download and install)
     - Open vlc, and select menu -- file -- open network
     - In the pop-up, enter the address: `tcp/h264://192.168.1.211:3333` and you will play the video on the in the vlc window
     - Alternatively, you can run `ffplay`
`ffplay tcp://192.168.1.211:3333 -vf "setpts=N/30" -fflags nobuffer -flags low_delay -framedrop` which runs in a console or ssh, but puts the play window on the monitor
6. Embedding video play in HTML
You will need to figure this out on your own.
7. Report.

When in doubt, see: [Stream Video over a Network with
rpicam-apps](https://www.raspberrypi.com/documentation/computers/camera_software.html#stream-video-over-a-network-with-rpicam-apps)


## Reference Material
- [Raspberry Pi Camera V2](https://www.raspberrypi.org/products/camera-module-v2/)
- [RPi Camera Software](https://www.raspberrypi.com/documentation/computers/camera_software.html)
- [rpicam-apps](https://www.raspberrypi.com/documentation/computers/camera_software.html#rpicam-apps)
- [Picamera2 Library](https://datasheets.raspberrypi.com/camera/picamera2-manual.pdf)
