### Video Streaming Recipe

This is derived from the [Raspberry Pi OS
Documentation](https://www.raspberrypi.com/documentation/computers/camera_software.html).

## Prep

- Make sure to load the most recent Pi OS (32 bit, 10/10/23)
- (Note: the camera software (libcamera) is pre-installed)

## With or without display attached to the pi

- Plug in your camera and test with:
  `libcamera-hello`
- With monitor, it will display a video stream for 5s
- Without monitor, running in ssh, it will display text for each frame
- If it is not working, consult the troubleshooting list in the docs

## Now with networking

- On the console (locally on the pi), or in ssh (remotely), run:
`libcamera-vid -t 0 --inline --listen -o tcp://192.168.1.211:3333`
- This puts the video on the network at 192.168.1.211:3333 on my network
- With a monitor attached it spawns a new window with video
- Without a monitor in ssh it shows a text description of each frame set

## Playing the video

- With a monitor, you can run (in a console window) the vlc player (comes installed with Pi OS)
`vlc tcp/h264://192.168.1.211:3333` 
- Without a monitor, you need to install the vlc player on your local laptop (download and install)
- Open vlc, and select menu -- file -- open network
- In the pop-up, enter the address: `tcp/h264://192.168.1.211:3333` and
you will play the video on the in the vlc window

- Alternatively, you can run `ffplay`
`ffplay tcp://192.168.1.211:3333 -vf "setpts=N/30" -fflags nobuffer -flags low_delay -framedrop` which runs in a console or ssh, but puts the play window on the monitor


## Embedding video play in HTML
You will need to figure this out on your own.

## Capturing stills on the pi

With the recent changes to the Pi OS, we will be using the tools
supported by `libcamera`. Included is an updated version of `picamera`
(now `picamera2`).

You can explore options for `libcamera` for capturing stills. In a
later quest, when decoding QR codes, it will be helpful to use python
as the execution environment for the workflow of camera stream -->
convert to gray --> test for QR code --> decode QR code.

### References
- [Raspberry Pi OS Camera](https://www.raspberrypi.com/documentation/computers/camera_software.html)
- [Picamera2](https://github.com/raspberrypi/picamera2)

