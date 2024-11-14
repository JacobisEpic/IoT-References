# Design Pattern – Node.js

[Node.js](https://nodejs.org/en/about/) lets you run asynchronous
event driven calls concurrently at your server side using
JavaScript. The conveniency of using Javascript lets a developer
program both the front-end and back-end of web apps using
JavaScript. JavaScript is king in web development. This is not
necessarily a win if you don't like JavaScript. However, the key to
Node.js is the extensive open source JavaScript modules available on
npm (node packaged modules). You can discover and use modules from
other developers -- no need to reinvent the wheel. This is a
convenience.

## Node Project
A node project will typically consists of three main components:
- the node program itself which has a file extension `*.js`
- the `node_modules` folder for installed modules
- the `package.json` file

The `package.json` file is not essential to running node, but comes in
handy when you want to transfer your code to a different machine. The
`package.json` file keeps track of the installed module dependencies
including version number so that when you port code to a different
machine (like you will when porting code from laptop to pi), you can
simply run `npm install` and all your module dependencies will install
with the right versions.

Example `package.json`:

```json
{
  "name": "stuff",
  "version": "1.0.0",
  "description": "stuff does stuff",
  "main": "stuff.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "emilylam",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.4",
    "socket.io": "^2.1.1"
  }
}
```

You can create a `package.json` by running the command `npm init` in
your project directory ([more on npm
init](https://docs.npmjs.com/getting-started/using-a-package.json)). `npm
init` runs through a questionaire to setup your `package.json`. There
are more attributes to
[package.json](https://docs.npmjs.com/files/package.json).

***Note for Pi Installations:*** You will need to update your RPi node
   installation to make node run successfully on the pi. The installed
   version is usually out of date.


## Modules
A typical node app will include some modules, whether built in,
created by you, or installed using npm. Think of this as the same as
including a library in c -- you cannot use a function in a module
without first including the module. Here are some common modules we
use and how to include them:

```js
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);
```

External modules or packages are installed to your local machine using
`npm install --save name-package`. The npm page for the package will
typically instruct on the installation process and how-to use the
package. Here's the
[socket.io](https://www.npmjs.com/package/socket.io) page as an
example. The `--save` flag updates the dependencies list in your
`package.json` file.

## Asynchronous 
Node.js, like JavaScript, is asynchronous, which means
code is not implemented sequentially but concurrently and independent
of each other. This is a hard concept to grasp and can get messy. But
there are some ways to control flow.


### Callbacks
You can enforce dependency and sequence through callbacks. A callback
is calling a second function within the first function so that the
second function runs after the first function completes. You can run
into "callback hell" -- nesting too many callbacks -- so use as
needed. An example of a callback follows:

```js
fs.readFile('/foo.txt', function(err, data) {
  // If an error occurred, handle it
  if(err) {
    console.log('Unknown Error');
    // This prints first
    return;
  }
  // This prints second
  console.log(data);
});
```

### Timers

A useful node module to help with control flow is the Timer
module. This module lets you schedule functions to call after some
time and also to call functions repeatedly on a set interval. Here is
the code snippet for setting up a function that is called every
1500ms:

```js
function intervalFunc() {
  console.log('Cant stop me now!');
}

setInterval(intervalFunc, 1500);
```

### Events
Much of node is built on an event-driven architecture, where some
objects, emitters, emit events that bound functions, objects, are be
called. For example, an event could be on client connection. So when a
client connects, listener functions execute. Here's an example using
events:

```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('an event occurred!');
});
myEmitter.emit('event');
```
The eventEmitter.on() method is used to register listeners, while the
eventEmitter.emit() method is used to trigger the event. When the
EventEmitter object emits an event, all of the functions attached to
that specific event are called synchronously.

This is just the basics of node. And there is much that we don't know
about node as well. But there are a plethora of resources on the
Internet if you want to take your node app beyond the basics.

### Serial port

We frequenlty want to connect an ESP32 as a sender with a laptop (or
Raspberri Pi) via USB (serial). The node server on the laptop can
connect to a serial port. There is a module called `serialport` that
you can install for use in node. This is one solution of many possible solutions. The
pattern is shown below. Make sure to install `serialport` using `npm`.


```
// Serial port example from design pattern
// Uses ESP code in folder: serial-esp-to-node-serialport

const {SerialPort} = require('serialport')
const port = new SerialPort({ path: '/dev/cu.usbserial-019FDB77', baudRate: 115200 });
const {ReadlineParser} = require('@serialport/parser-readline');
const parser = port.pipe(new ReadlineParser({ delimiter: '\n' }));

// Read the port data
port.on("open", () => {
  console.log('Serial port now open');
});
parser.on('data', data =>{
  console.log('The word from ESP32:', data);
});

```

You of course will need to match the baud rate and port of your ESP32
with that of the script. Run the node server and the ESP console in
different command windows/shells.

There are many other similar examples available to emulate online. 


## Running Node
Running node is simply `node stuff.js`.

## References
- [Node.js](https://www.w3schools.com/nodejs/default.asp)
- [JavaScript](https://www.w3schools.com/js/default.asp)
- [Node.js Event Loop](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)
- [Node Timer Module](https://nodejs.org/en/docs/guides/timers-in-node/)
- [Built-in-modules](https://www.w3schools.com/nodejs/ref_modules.asp)
- [Node serialport](https://serialport.io/docs/api-serialport)
- [Node.js via Serial Port](https://medium.com/@machadogj/arduino-and-node-js-via-serial-port-bcf9691fab6a)
- [Serial to Node Example Code](https://github.com/BU-EC444/04-Code-Examples/tree/main/serial-esp-to-node-serialport)