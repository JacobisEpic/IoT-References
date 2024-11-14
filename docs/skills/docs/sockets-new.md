# Network Sockets

This is where your prior knowledge of computer networking would come
in handy... The Socket is an IP protocol metaphors and construct for
one-to-one connections. If you want to get data from A to B, then the
socket is the fundamental building block in your software/network
stack.

You are not going to learn all the networking details here, but rather
enough to build a working example to exploit later. With some
experience you will find that with most machine-to-machine
communications, all of your trouble and effort will go into handling
errors and exceptions and what to do about them. But that's for later.

## Basic idea of sockets

- We're considering IP (Internet Protocol) sockets
- A process requests the creation of a socket resulting in a socket descriptor handle
- A socket address consists of an IP address and port number
- Each endpoint (A and B) will have their own socket address for each other
- The way you work with the sockets is via host-specific API (enter ESP32 APIs)
- Sockets are used with IP, UDP, TCP


Here is the example from the Wikipedia page on network programming:

```Socket socket = getSocket(type = "TCP")
connect(socket, address = "1.2.3.4", port = "80")
send(socket, "Hello, world!")
close(socket)
```

Also, there are different types of sockets called datagram, stream,
and raw. We concern mostly with datagrams via UDP and stream types
via TCP.

But what really matters for building systems is how to interface from
your particular programming environment. More often than not, an
endpoint process will deal with the complexities of socket
programming (e.g., via some other protocols such as HTTP).

Have a look at the Espressif APIs and examples as a starting
point. Here is what you will find:

TBD -- sockets exmaple to work through

<p align="center">
<img src="/docs/images/tbd.jpg" width="50%">
</p>
<p align="center">
<i> Sockets </i>
</p>

## Assignment
1. Assuming that you have worked through the WiFi configuration examples, design a program that will send data from point A to B.
2. Implement and send 'hello world' between endpoints (a chat)
3. Implement a function that will send some unit of data as JSON from A to B where data at B are saved to a file.
4. Write up, report, and show evidence that this all works


## Reference material
- [Network Sockets](https://en.wikipedia.org/wiki/Network_socket)
- [Node.js UDP](https://nodejs.org/api/dgram.html)
- [ESP Sockets Examples](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sockets)
- [ESP32 Github: UDP Multicast](https://github.com/espressif/esp-idf/tree/51a4b4ba2716e7b57aeafa804c48f927d8d3895a/examples/protocols/udp_multicast)
