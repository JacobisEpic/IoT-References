# Raspberry Pi

In this skill you will bring up a Raspberry Pi (RPi) Zero W and
establish that it can connect to a wireless network and host a Node.js
server.

Unless you have a new device, you will find an existing
installation. Your job is to reinstall from scratch with a clean
system.

<p align="center">
<img src="/docs/images/RPi0.jpg" width="50%">
</p>
<p align="center">
<i>RPi Zero</i>
</p>

## Assignment (with keyboard, mouse, and monitor)
1. Download the latest firmware for the RPi (link below)
2. Format your SD card and install Raspberry Pi OS (formerly Rasbian)
3. Boot the pi and then follow the instructions to configure the pi (note: defining a user with ID that is not `pi` will cause problems
for installing the pi-cam later)
4. You will configure the pi to access to your team's wifi router during boot up
5. Install node.js (see below)


## Assignment ("headless," without keyboard, mouse, and monitor)
1. Follow the instructions for setting up remote access to the pi [Remote Access}(https://www.raspberrypi.com/documentation/computers/remote-access.html)
2. Download the latest firmware for the RPi (link below)
3. Format your SD card and install Raspberry Pi OS (formerly Rasbian) **do not boot the pi yet**
4. Use the template files in /skills/docs/headless/ (modified for your group number), adding them to the boot partition on your
SD card
5. Make sure your router is configured and running per your group number and credentials with WPA2
6. Boot the pi (could take a few min). It will connect to your designated router with credentials set by you
7. Find your device IP address on the local subnet (use the router web interface to find the pi address)
8. SSH into your pi
9. Install node.js (see below)

## Installing Node
Install node.js headless: use [These Instructions with Method 1](https://www.golinuxcloud.com/install-nodejs-and-npm-on-raspberry-pi/) summarized below:

- Enable NodeSource Repository

```
sudo curl -fsSL https://deb.nodesource.com/setup_19.x | bash - &&\

```

- Install NodeJS

```
sudo apt-get install -y nodejs
```
- Verify installation

```
node --version
npm --version
```

- Now Use git on the pi to pull files from your team repo
- ssh into the pi in a terminal window:
- Pull the basic hello world example

Do once (example -- use your repo not mine):
```
git clone https://github.com/BU-EC444/Little-Thomas
```
Do to refresh with latest code
```
git pull https://github.com/BU-EC444/Little-Thomas
```

- Start node.js with your hello world example, demonstrate access from a different computer on the subnet
- Post evidence that it works for the skill


## Notes on using git to pull node applications
- We recommend that you test node.js code on your laptop before
deploying on the RPi.
- Using git on the RPi will greatly simplify deploying code on the RPi
  as you will not need to write and debug on the RPi.
  - Write the code on your laptop
  - Push to your git repo
  - Pull from the RPi to transfer working files to the RPi


## Reference Material
- [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
- [Remote Access with SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/)
- [Downloads for Raspberry Pi OS](https://www.raspberrypi.org/downloads/)
- [OS Installation Guide](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)
- [Node.js](https://nodejs.org/en/)
- [Adafruit install](https://learn.adafruit.com/raspberry-pi-zero-creation)




