# Laser Tag

In laser tag, typically two teams hunt each other inside a dark
warehouse with indoor structures in which to hide and target the
opposing team.  Scoring is achieved when one teams' beams is
successfully received and recorded by an opponent. When this happens,
the opponent player is disabled for a time or until the game resets.

We'll use this connected system to integrate some of our concepts: (a)
IR TX-RX, (b) leader election, (c) score aggregation and report-out.

Here's the scenario: configure the ESP32s to have network connectivity
(BLE or WiFi) to be able to report scores to a server (laptop or
RPi). Attach the IR PD and the IR transmitter (looks like an LED) to
the breadboard. Make sure to isolate (so you don't disable
yourself). Establish a code for transmission that is unique to your
device (a simple ID will do). Add a button.  On button push, a device
will emit the code. Meanwhile if a device receives some one else's
code, it reports this 'hit' to the server process on the laptop (with
who did the hit).  The game is timed.  After a device is 'hit' three
times (or some constant), the device is disabled. The game ends when
one team exhausts all of it's active players.

On reset the game starts by first selecting a leader (leader
election), then the leader will divide the set of devices to create
two teams (red and blue). Each device will need LEDs to indicate which
team they are on. The alphanumeric display should be used to indicate
the current number of hits received.

The service process will be used to aggregate scores by each device in
real time with web client access to display the game score leaderboard.


<img src="/docs/images/lasertag.png" width="100%" /></center>
<center>Laser Tag Components</center>

## Assignment
1. Design and build this system. State any game assumptions.
2. Agree on target performance as assessment criteria. Be complete, but keep it simple and objective.
2. Demonstrate your solution
3. Write up a description of how you built your solution. Include
concepts, modules, APIs, tools, etc.
4. Submit a < 90s video of your report. Everyone must be on the video.

