# Design Pattern – Socket.IO

There are many ways to pass information between your front-end clients
(browser, HTML) and your back-end server (Node.js server). We've found
the [Socket.IO](https://socket.io) module to be a reliable method in
doing this for both binary and JSON encoded data. However, you are
free to explore your own solutions; this is a starting point.

From the [Socket.IO](https://socket.io/docs/) website:

> Socket.IO enables real-time, bidirectional and event-based
communication.  It works on every platform, browser or device,
focusing equally on reliability and speed.

In essence, you will need to create a "socket" between your backend
(Node.js code) and frontend (HTML code). The code below is available
on our course repo:
[code-examples](https://github.com/BU-EC444/code-examples).

<p align="center">
<img src="/docs/images/socketio-dataflow.png" width="55%">
</p>
<p align="center">
<i></i>
</p>

## Node.js

In this example, we've created some dummy data imitating information
streaming to the server. In your actual projects, you'll be streaming
data via the serial port, maybe UDP sockets, or something else.

A few things are happening:
  1. Http server @ localhost:3000
  2. Every time a client connects, a new socket is created
  3. A webpage is served to the connected device
  4. *Streamed* data are emitted onto the `message` event to all connected sockets

And remember, Node.js is asynchronous so it doesn't really matter where functions are called.

```js
// Modules
var express = require('express');
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

// Iterate from 0 to 10 (then loop) at 1 second intervals
var i = 0;
setInterval( function() {
  console.log('Read:', i);    // Log to console
  io.emit('message', i);      // 4. Emit to message event
  i++;
  if (i > 10) {i=0;}
}, 1000);

// 3. Points to index.html to serve webpage
app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

// 2. User socket connection
io.on('connection', function(socket){
  console.log('a user connected');
  socket.on('disconnect', function(){
    console.log('user disconnected');
  });
});

// 1. Listening on localhost:3000
http.listen(3000, function() {
  console.log('listening on *:3000');
});
```


## HTML

Just like the node.js code, you'll need to link to the socket.io
module. This is done with a javascript code block: `<script
src="/socket.io/socket.io.js"></script>.` In addition, you will also
write javascript to create a socket and listen to the `message`
event. Then, a HTML element attribute is called to display the data.

``` html
<!-- client side -->

<!doctype html>
<html>

<!-- HTML HEAD -->
<head>
	<title>TEST</title>
	<!-- Source for Socket.io - this one is local -->
	<script src="/socket.io/socket.io.js"></script>

</head>

<body>
	<!-- HTML layout -->
  <h1>Hello world -- test 1, 2, 3</h1> <br>
	<div> Received: <p id="message_disp"></p> </div>

	<!-- Script to handle socket -->
	<script>
		var index = 0;
		var socket = io();
		socket.on('message', function(msg){
			console.log(msg);
			document.getElementById("message_disp").innerHTML = msg;
		});
	</script>

</body>

</html>
```

## Running the example code

On our course repo, you'll find a [Socket.IO
example](https://github.com/BU-EC444/04-Code-Examples/tree/master/node-socketio)
that works as is.

- First, install the modules by running `npm install`
- Next, start your server by running `node socketio-example.js`
- Then, open up a browser window to `http://localhost:3000`
- Finally, you should get the below output:

<p align="center">
<img src="/docs/images/socketio-html.png" width="100%">
</p>
<p align="center">
<i></i>
</p>


## References
- [Socket.IO](https://socket.io)
- [Socket.IO Documents](https://socket.io/docs/)
- [Socket.IO Example](https://github.com/BU-EC444/04-Code-Examples/tree/master/node-socketio)
