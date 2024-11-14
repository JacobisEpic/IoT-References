# Recipe -- Pi Camera

Adapted from: [Build a Respberry Pi Webcam Service in Minutes](https://pimylifeup.com/raspberry-pi-webcam-server/).

Last update: 2023-03-20 <br>
Tested with Pi Zero W (hardware ca 2019)

## Preliminaries

1. Have a local router with known SSID and login credentials
2. Download the Raspberry Pi installer
3. Flash the SD card with the recommended OS (currently Debian Bullseye 32-bit, March 2023)
4. DO NOT create your own credentials using the installer configuration tool (this creates a login with the non-root credentials)
4. Follow instructions for headless install (requires setting up SSH and SSID and credentials before booting from the SD card). See the recipe for headless install on the pi. 
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
6. Reboot with
```
sudo reboot
```

## Installing the camera gunk

1. Install packages required for the build
```
sudo apt install autoconf automake build-essential pkgconf libtool git libzip-dev \
libjpeg-dev gettext libmicrohttpd-dev libavformat-dev libavcodec-dev libavutil-dev \
libswscale-dev libavdevice-dev default-libmysqlclient-dev libpq-dev libsqlite3-dev \
libwebp-dev
```

2. The motion install fails to install log files. Here is the fix. First create the problem files:
```
sudo mkdir /var/log/motion
sudo touch /var/log/motion/motion.log
```
3. Then change permissions and ownership of the folder and log file. This allows the files to be rwx (executed as) root
```
sudo chmod ugo+rwx /var/log/motion
sudo chmod ugo+rwx /var/log/motion/motion.log
sudo chown root /var/log/motion
sudo chown root /var/log/motion/motion.log
```

4. Now install motion (if successful, it starts motion automatically)
```
sudo apt-get install motion
```

5. If there is no error, you need to edit the config files and then either restart motion or reboot.
Open  the `motion` config file using the nano linux editor:
```
sudo nano /etc/motion/motion.conf
```
6. Make sure these are set as follows (save and exit with `cntrl-X Y`)
```
daemon on
stream_localhost off
movie_output off
stream_maxrate 15
framerate 100
width 640
height 480
```
7. Now reboot or kill the motion process. Identify the process ID with:
```
ps -aux | grep motion
```

8. Then kill it and restart (alternatively you can reboot)
```
sudo kill -9 [the ID number]
```

9. Start motion as root 
```
sudo motion
```
10. Test the camera output from your laptop (on the same subnet) with
```
http://192.168.1.10:8081
```

## Other notes
- Motion will run as root with this set of steps (better for security purposes to run as own user)
- Motion is not started by default at boot time. Need to manually start or use setup command for this
- Use `sudo` to overcome permission exceptions
- Make sure the laptop is on the same subnet
- Can set DDNS to access the `motion` http address and port (http://yourdomain.com:8081)

