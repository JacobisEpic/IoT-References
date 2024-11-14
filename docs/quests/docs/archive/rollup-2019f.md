# Rollup -- Capture the Flag Crawler-Style

**Plan to run demos with routers but no internet (wired) connection**


In this quest your goal is to send your crawler through a course,
passing checkpoints, and then to capture a flag. It's a race.  The
course is illustrated below.

<center><img src="/docs/images/course2019.png" width="100%" /></center>
<center>  Capture the Flag Race Course Layout</center>

This quest rolls up earlier quests. The challenge will be to integrate
the pieces.

## Required elements
- Web interface including
  - For steering and controlling car speed and direction
  - Showing current and past "splits" recorded on the course by your crawler and
  written to the RPi database
  - Live streaming video coming from a webcam on the RPi on the crawler

- Crawler including
  - Range sensors for tracking wall
  - Collision sensor on front
  - PID control on set-point speed (forward direction, not required for reverse)
  - IR receiver
  - Alpha display showing most recent split (time)

- New functions
  - Web streaming from RPi on vehicle
  - Left and right turns at corners -- follow walls
  - Triggered start and stop signals based on signal from beacon (green--go, red--stop, yellow--slow down)
  - Record split time when reach each beacon
  - Remote driving when reach last beacon
  - Decode QR code

The overall system architecture, flow, and crawler components are shown below.

<center><img src="/docs/images/crawler2019.png" width="80%" /></center>
<center>  System Architecture, Flow, and Crawler Parts</center>


The beacon behavior is illustrated in the figure below.

<center><img src="/docs/images/stoplight.png" width="60%" /></center>
<center>  Beacon/Stoplight Behavior</center>


**We will provide programmed beacons.**


## Running the course

Two cars will start at the initial beacon/signal. One will go left,
the other right. Each crawler will navigate the walls until
encountering the beacon. When detected, the crawler will log the time
of discovery of the beacon and then display this as split time
(logging to the DB on the RPi). If the signal is not green, the car
will wait until a green signal is received.

The crawler will continue until reaching the third beacon. At this
point, a human driver can take over driving to bring the car to the
flag (QR code). This will be achieved using the web-based driving
control and the streaming video from the crawler to the browser.

Once in range of the QR code, the code should be decoded (either by
the RPi or by the client/laptop/browser and the "capture" time is
recorded as the final course time. Lowest time is the champion.

Best split times should be displayed on the client browser based on a
query to the database.

<center><img src="/docs/images/gsu-alley-course.png" width="80%" /></center>
<center>  GSU Alley Course -- you will either go left or right</center>

## Rubric  
- [Updated Objective Criteria](/docs/rubrics/docs/rollup-rubric.pdf)
- Note that the usual qualitative criteria apply


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions, but
   - Make video and report suitable for sharing during interview
4. Investigative question: None


## Reference material
- Prior quests and skills

## Beacons/Traffic Lights

We will use four beacons running at 1200 Baud. These beacons are
capable of transmitting and receiving IR data; however, you will use
them in this quest as a simple beacon radiating their IDs and light
color. The LEDs will show their current state.

The payload will contain 4 bytes: START (0x1B), color ('R','Y','G'), ID (1-3),
and 1 byte XOR checksum. (Note: `0x1B` corresponds to ASCII ESC.)
Also, you are not required to use the checksum.

**Beacons will be located on the floor, pointing towards oncoming
  traffic.** See the illustration below for spacing.

<center><img src="/docs/images/spacing.png" width="60%" /></center>
<center>IR Beacon Placement</center>



Indicator Color    | Color
------------       | -------------
RED                | 'R'
YELLOW             | 'Y'
GREEN              | 'G'

The beacons use a 33 Ohm resistor (or three 100 ohm resistors --
brown-black-brown -- in parallel) which increases their intensity and
range to about 1.5 m.


## Beacon code
+ To be provided [Code](https://github.com/BU-EC444/code-examples/tree/master/ir-car-beacon-capture)


<center><img src="/docs/images/ir-beacon.jpg" width="40%" /></center>
<center>IR Beacon/Stoplight</center>
