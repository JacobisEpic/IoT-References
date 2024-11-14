# Smahrt Key

The smart key works like this. You carry it with you, and when you
want to unlock something you press the button and it transmits a short
range "near field" message to a hub. And then the hub unlocks
something and logs your presence, and sends an acknowledgement back to
the smart key.  Security is provided by the NFC and perhaps some
encryption on top of the message.

<p align="center">
<img src="/docs/images/smart-key1.png" width="100%" />
</p>
<p align="center">
<i> Smart Key System Components</i>
</p>


Your job is to build and program the key for each of your team members and then
build and program the hub.

This quest builds on a number of skills you should have completed by now:
- IR TX-RX
- HTTPD on the ESP32
- Node.js

But introduces several new ones:
- Persistence/databases
- Security

Also, you are working with a system of multiple devices.

Here are some features that are required in your solution
- Database logs each key-open request including time stamp, fob ID,
 hub ID, name of person with key
- Queries to database will reveal
  - Time series for (key ID)
  - Presence (indicates if a devices has 'checked-in') to a room
- Button press received at hub is passed to Pi where it is validated. Pi contacts the fob by WiFi and
then fob turns on green light to indicate that key is unlocked


Notes:

- ***A key-open request*** is a successful exchange of data by a fob ID at a hob ID
- You may have multiple hubs in the system; therefore, each hub will have a unique ID
- Your "code" can be what your team defines. Consider a 4 digit number (PIN) or passphrase (text string)

<p align="center">
<img src="/images/smart-key-flow1.png" width="100%" />
</p>
<p align="center">
<i> Smart Key System Data Flow</i>
</p>

Conveniently, the design of the fob is the same as the IR TX/RX beacon
used in Quest 4. Shown below.

<p align="center">
<img src="/images/ir-beacon.jpg" width="80%" />
</p>
<p align="center">
<i> Smart Key Fob Components</i>
</p>

## Assignment
1. Design and build this system. 
2. Demonstrate your solution
3. Report
4. Video

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
