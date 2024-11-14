# Online Appliance Nugget

Recap of some common questions we've received throughout the exploration of quest 3.

<p align="center">
<img src="/docs/images/toaster.png" width="80%">
</p>
<p align="center">
<i>Toaster</>
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
<img src="/docs/images/local-esp-network.png" width="80%">
</p>
<p align="center">
<i>Local ESP Network</i>
</p>

While the WiFi and httpd modules will bring the ESP32 onto a local
network, it is up to the router to channel the device to the
internet. We use port forwarding to route traffic to the right local
device.

<p align="center">
<img src="/docs/images/port-forwarding.png" width="80%">
</p>
<p align="center">
<i>Port Forwarding</i>

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
<img src="../../images/server-client.png" width="80%">
</p>
<p align="center">
<i>Server-CLient</>
</p>

# Quest 3 In-Class


In-Class assignment
1. Provide a block diagram of the structure of your system indicating major components and data flow
2. Provide a flowchart of how you propose to program the ESP32 and the other components of the system
3. Identify any unknowns
4. Report your results to your Quest 3 repo. Be prepared to discuss
