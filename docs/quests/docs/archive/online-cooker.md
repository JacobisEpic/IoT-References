# Online Appliance

There are many possible IoT appliances. We thought of a smart toaster,
smart rice cooker, smart coffee maker, etc., etc. But we couldn't
decide on one type, so we abstracted the qualities of any smart
thingamajig.

The key features of a smart appliance are going to be:
- Does something in your home, possibly while you are away 
- Scheduled (***has a clock with clock logic***)
- Control (turns things on and off -- "cooking")
- Senses something (temperature of burner) 
- Provides feedback (remote web camera) 
- Remotely programmable (network access, IP protocols)
- Uses alphanumeric display

A typical use case would be: I connect to my device from work, control
an actuator (servo) to put coffee into the hopper, ***set a time*** to turn
on the brewing. The brewing starts at some programmed time, the
brewing stops.  If I check on status I will get a report on the state
of the machine, temperature, and a web stream of images of the brew.

<p align="center">
<img src="/docs/images/toaster.png" width="100%" />
</p>
<p align="center">
<i> Smart Appliance Scenario</i>
</p>

<center>Smart Appliance</center>

## Strategy 

As with all of these assignments, there are a lot of moving parts, but
each part is not as complex as it sounds. We approach this problem
with the following breakdown:

- Bring up your router (skill)
- Get the ESP32 to talk to a WiFi access point to establsh connectivity (WiFi skill)
- Establish how you will transfer data from the ESP32 to a web client
or server (could be colocated on your laptop). We are recommending
using an HTTP server on the ESP32 (there is a basic demo for this) and
using GET and POST/PUT from your client (or server). 
- Integrate control of your local devices (servo, reading temperature, ***time***)
with the HTTP server on the ESP32
- Design the web client (page) to provide control (buttons, display of
video). We recommend doing this via a local node.js server with calls
to your ESP32 HTTP server, which makes the location of your hosting
server independent of your laptop (when we move this to the RPi
later). Alternatively your can write javascript at your client.
- Bring up separate RPi as an independent webcam streaming to your client
- The above is a recommendation but there are certainly different ways
  of doing this.

## Assignment
1. Decide an appliance type and use case (e.g., coffee maker). This will
advise the behavior of your system. You can pick any one in the illustration. Define the
behavior of the device as a state diagram (some aspect of the system). ***Note:*** you are not actually
building a real appliance, but you ***are*** designing and implementing all of the control and actuation.
2. List actuators you will build (at least one actuation and one sensing). This will define
what you need to communicate across the network (video is not counted as sensing here and is separate)
3. Include a remote user interface to control the device (client browser control)
4. Maintain state somewhere in the system -- best if on the device; this includes your scheduling
5. Bring up the RPi with web cam to observe your device. This should deliver data to your remote client.
6. The usual report and video


## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Does A  |  |  1     | |
| Does B  |  |  1     | |
| Does C  |  |  1     | |
| Does D  |  |  1     | |
| Does E  |  |  1     | |
| Does F  |  |  1     | |
| Does G  |  |  1     | |

