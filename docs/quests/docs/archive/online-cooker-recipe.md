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

<center>Smart Appliance Scenario</center>

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
- Design the web client (page) to provide control (buttons, display of video). We recommend doing this via a local node.js server
with calls to your ESP32 HTTP server, which makes the location of your hosting server independent of your laptop (when we move this to the RPi later). Alternatively your can write javascript at your client. 
- Bring up separate RPi as an independent webcam streaming to your client

- The above is a recommendation but there are certainly different ways
  of doing this.

Here is an illustration of the basic strategy:

<p align="center">
<img src="/docs/images/quest3-overview.jpg" width="100%" />
</p>
<p align="center">
<i>Strategy Overview </i>
</p>


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


## Reference material
- [Additional Guidance on this Quest](/progress/nuggets/quest3-nugget)
- [WiFi Station Example](https://github.com/espressif/esp-idf/tree/master/examples/wifi/getting_started/station)
- [ESP32 HTTP Server Example](https://github.com/espressif/esp-idf/tree/master/examples/protocols/http_server/simple)
- Router Config Skill
- WiFi Skill
- DYNDNS Skill
- RPi Skill
- Web Camera Skill


## Optional features
- Include a local alphanumeric display
- Include interent power switch and IFTTT



# Online Appliance Nugget

Recap of some common questions we've received throughout the exploration of quest 3.

<p align="center">
<img src="/docs/images/toaster.png" width="80%" />
</p>
<p align="center">
<i> Toaster</i>
</p>


### Conventional Appliance
A conventional appliance usually consist of a micro + actuators and
sensors. This is similar to the psudeo-mechanical and swiss army
knife. But for this quest: one actuator and one sensor. For the
toaster example, the micro is the ESP32, the actuator is a servo to
pop the toast after the timer goes off, the sensor is to measure and
regulate heating, and inputs can be buttons.

<p align="center">
<img src="/docs/images/conven-toaster.png" width="80%" />
</p>
<p align="center">
<i> Conventional Toaster</i>
</p>

### Bringing the ESP32 Online

A smart appliance connects to the web and lets you service and observe
the appliance remotely. This is the backbone of IOT. The ESP32 can
connect and communicate to a wireless local access network (WLAN)
using WiFi and traditional UDP/TCP sockets. We will not be doing
barebones UDP/TCP sockets programming. Instead, the ESP32 provides a
lightweight http server/client API
([server](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/protocols/esp_http_server.html),
[client](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/protocols/esp_http_client.html))
that we can call GET and POST/PUT requests to communicate between
devices. You are free to explore different protocols but this is what
we are recommending.

<p align="center">
<img src="/docs/images/local-esp-network.png" width="80%" />
</p>
<p align="center">
<i> </i>
</p>


While the WiFi and httpd modules will bring the ESP32 onto a local
network, it is up to the router to channel the device to the
internet. We use port forwarding to route traffic to the right local
device.

<p align="center">
<img src="/docs/images/port-forwarding.png" width="80%" />
</p>
<p align="center">
<i> </i>
</p>

Example: if you run a server at port 8080 on the Pi, a device on the
internet could reach the server on the Pi at 128.197.53.92:2222.

A Dynamic Domain Name System (DDNS) service keeps track of the
router's public IP address, which can change, and assigns an alias to
it.

### Server-Client Relationship

While the server and client can be at the same location
(physically). It is often convenient to host the server at a remote
host and use any client to access the server. This is the
middle-server idea we propose. This middle-server serves as the main
contact point maintaining relationships with the client (outside the
local network), the ESP32, the webcam, and possibly IFTTT (to the
Smart Plug). In future quests, you will also have your server maintain
a database. We build the server using Node.js but you can also build
this on Python or any other backend language. We like Node.js because
you can also embed javascript for front-end stuff (HTML) and there are
a lot of open source modules to use.

<p align="center">
<img src="/docs/images/server-client.png" width="80%" />
</p>
<p align="center">
<i> </i>
</p>


# Quest 3 In-Class


In-Class assignment
1. Provide a block diagram of the structure of your system indicating major components and data flow
2. Provide a flowchart of how you propose to program the ESP32 and the other components of the system
3. Identify any unknowns
4. Report your results to your Quest 3 repo. Be prepared to discuss

<p align="center">
<img src="/docs/images/quest3.png" width="100%" />
</p>
<p align="center">
<i> </i>
</p>
