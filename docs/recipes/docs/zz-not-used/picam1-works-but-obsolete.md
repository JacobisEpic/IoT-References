# Recipe -- Pi Camera

Adapted from: [Build a Respberry Pi Webcam Service in Minutes](https://pimylifeup.com/raspberry-pi-webcam-server/).

Last update: 2023-03-17 <br>
Tested with Pi Zero W (hardware ca 2019)

## Preliminaries

1. Have a local router with known SSID and login credentials
2. Download the Raspberry Pi installer
3. Flash the SD card with the recommended OS (currently Debian Bullseye 32-bit, March 2023)
4. Follow instructions for headless install (requires setting up SSH and SSID and credentials before booting from the SD card)
5. Put the SD card into the pi and power up (initial boot can take 5 min)
6. Connect from your laptop to your router SSID above
7. Log in to your router and identify the IP address of your pi (lets say it's `192.168.1.10`)
8. Open a command window and log into the pi with credentials used in build (`pi/smart`)
```
ssh pi@192.168.1.10
```
9. Update the software to the latest version
```
sudo apt update
sudo apt upgrade
```

## Installing the camera 
1. Unplug the power and attach the camera. Carefully separate the dark clamp and 
slip the ribbon (shiny side down) into the connector. Press the clamp towards the connector.

2. Configure the camera -- enable the camera using `raspi-config` -- select 'interfaces' and then select 'legacy camera.' Save with `cntrl-X Y`.
```
sudo raspi-config
```
3. Wait for the reboot... and log-in again

4. With camera attached and running, add the camera to modules using the nano editor
```
sudo nano /etc/modules
```
And add as the last line
```
bcm2835-v4l2
```
5. Alternatively, you can run this command
```
sudo modprobe bcm2835-v4l2
``` 
4. Reboot with
```
sudo reboot
```

## Installing the camera gunk

1. Install packages for the required for the build
```
sudo apt install autoconf automake build-essential pkgconf libtool git libzip-dev \
libjpeg-dev gettext libmicrohttpd-dev libavformat-dev libavcodec-dev libavutil-dev \
libswscale-dev libavdevice-dev default-libmysqlclient-dev libpq-dev libsqlite3-dev \
libwebp-dev
```

2. Download `motion` debian (deb) file for Rasbian Buster from GitHub using `wget` and install using `dpkg` 
```
sudo wget https://github.com/Motion-Project/motion/releases/download/release-4.5.1/\
$(lsb_release -cs)_motion_4.5.1-1_$(dpkg --print-architecture).deb

sudo dpkg -i $(lsb_release -cs)_motion_4.5.1-1_$(dpkg --print-architecture).deb
```
3. This build fails on creating the log files and folder. Here is the fix. First create the problem files:
```
sudo mkdir /var/log/motion
sudo touch /var/log/motion/motion.log
```
4. Then change permissions and ownership of the folder and log file. This allows the files to be rwx (executed as) root
```
sudo chmod ugo+rwx /var/log/motion
sudo chmod ugo+rwx /var/log/motion/motion.log
sudo chown root /var/log/motion
sudo chown root /var/log/motion/motion.log
```
5. Note that the clean build overwrites the log files and folder and will continue to frustrate you if you use `apt-get purge`. Don't do that.
The fix is to use `remove` which seems to preserve the folders. Run this:
```
sudo apt-get remove motion
```
6. Now reinstall -- the build should complete correctly with the folders set up earlier (installs different version though)
```
sudo apt-get install motion
```
7. A successful build will create a log file with stuff in it. But you are not done yet

8. Open  the `motion` config file using the nano linux editor
```
sudo nano /etc/motion/motion.conf
```
9. Make sure these are set as follows (save and exit with `cntrl-X Y`)
```
daemon on
stream_localhost off
movie_output off
stream_maxrate 15
framerate 100
width 640
height 480
```
10. Start `motion` as root 
```
sudo motion
```
11. Test the camera output from your laptop (on the same subnet) with
```
http://192.168.1.103:8081
```

## Other notes
- Motion will run as root with this set of steps (better for security purposes to run as own user)
- Motion is not started by default at boot time. Need to manually start or use setup command for this
- Use `sudo` to overcome permission exceptions
- Make sure the laptop is on the same subnet
- Can set DDNS to access the `motion` http address and port (http://yourdomain.com:8081)

