# Bring up and demonstrate HTTPD on the ESP32 

HTTP (HyperTex Transfer Protocol) is a protocol built on top of TCP/IP
for transfering objects (text, images, etc.) between computers and is
a cornerstone for enabling web applications. Typically a client (web
browser) generates requesst which are passed to a server (HTTP daemon
of server). The server receives the request and through local (to the
server) processing and access to files, returns a response that is
sent back to the client where it is rendered by the client.

Node.js is an example of an evironment that runs an HTTPD but there
are many more. The advantage of using HTTP over IP sockets is the
abstraction of some of the details of network programming allowing you
to write applications more quickly. Of course there are cases where
going to sockets makes sense, but for now we will go at it with HTTP.

In this skill you will bring up the ESP32 HTTPD simple example and
demonstrate. This skill assumes that you have set up your routers and
configured your wifi.

Note: this example uses curl to generate the HTTP request. You can
continue to use curl, or use your own alternative (e.g., Node.js)

## Assignment
1. Bring up the Hello World example 
2. Modify the code to return the state of button push for a pushbutton on one of hte GPIO pins
3. Modify the code to change the state of an LED on one of hte GPIO pins
4. Report 

## Reference material
- [ESP32 HTTPD Example](https://github.com/espressif/esp-idf/tree/master/examples/protocols/http_server/simple)

