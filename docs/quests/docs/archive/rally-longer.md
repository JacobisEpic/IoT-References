# Rally -- racing a course with checkpoints

Rally is a sporting activity involving cars, competition, navigation,
and timing. A perfect rollup of the skills so far.

<p align="center">
<img src="/docs/images/rally.jpg" width="40%">
</p>
<p align="center">
<i>  Rally Car <br> (By Harpagornis - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=48987237)
</i>
</p>

In this quest your goal is to send your car through a course, passing
checkpoints, logging your time and distance, and arriving at a finish
line.  The components are illustrated below.

<p align="center">
<img src="/docs/images/rally-sol.png" width="80%">
</p>
<p align="center">
<i>Rally Components</i>
</p>

This quest rolls up earlier quests. The challenge will be to integrate
the pieces.

## Required elements
- Web interface including
  - For steering and controlling car speed and directiony
  - Logging of time elapsed from start, through each checkpoint, and to the finish for multiple runs 
  - Data are logged on a RPi-hosted database
  - Preset queries to the database result in computation and display of average checkpoint time on web page
  - Live streaming video coming from a webcam on the RPi on the buggy

- Buggy including
  - Range sensors for collision avoidance on sides
  - Collision sensor on front
  - PID control on set-point speed (forward direction, not required for reverse)
  - IR receiver to trigger start of race
  - Alpha display showing most recent split (time)
  - Decode QR code at checkpoints


## Running the course

There will be two identical courses set up. Two cars can start at the
initial beacon/signal. One will go left, the other right. Each crawler
will drive to the next checkpoint. At the checkpoint, the on-board Rpi
and camera will decode the ID of the checkpoint and log this to the
database. The goal is to have the lowest average transit time logged
(of all checkpoint-checkpoint transits). After each transit, the
current average transit time should be displayed on the alpha display.

The crawler must not hit any objects on the course or the run will be
disqualified. Remote driving is allowed; however, the car must be run
using a predetermined setpoint on a PID speed contoller. At each
checkpoint, the next checkpoint will indicate a left turn, a right
turn, or a full turn (back to the originating checkpoint). This
sequence will be provided to the race teams prior to starting the
course. We recommend designing a control sequence to automate these
turns, to save time over a manual method.

**Plan to run demos with routers but no internet (wired) connection**



<p align="center">
<img src="/docs/images/gsu-rally.png" width="80%">
</p>
<p align="center">
<i>GSU Alley Course -- you will either go left or right</i>
</p>


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work on Race Day
3. Reporting as per quest reporting instructions, but ***make video and report suitable for sharing during interview***


## Reference material
- Prior quests and skills
- [Rally (Wikipedia)](https://en.wikipedia.org/wiki/Rallying)

## Rubric  
| Objective criteria (0/1, 1=met)                                                                 | Rating | Max |
| ----------------------------------------------------------------------------------------------- | ------ | --- |
| Car is controlled through web interface with L, R, F, R, stop, and speed setpoint controls      |        | 1   |
| Video from car incorporated in single browser frame with driving controls                       |        | 1   |
| Client web interface to query for race statistics                                               |        | 1   |
| Car is controlled remotely from URL and drives successfully including L, R, F, R, stop controls |        | 1   |
| Each QR code checkpoint is visited by car and decoded in program                                |        | 1   |
| Successfully executes at least 50% of self-turns                                                |        | 1   |
| Uses PID control for constant speed between checkpoints.                                        |        | 1   |
| Logs transit times into RPi database                                                            |        | 1   |
| Starts course with IR green light                                                               |        | 1   |
| Functional range sensors. Collision avoidance used; no collisions with any objects on course    |        | 1   |
| Displays current average transit time on alpha display                                          |        | 1   |
| Completes the course without nudges or touches                                


## Beacons/Starting the Course

We will will provide starting beacons running at 1200 Baud. These beacons are
capable of transmitting and receiving IR data; however, you will use
them in this quest as a simple beacon radiating their IDs and light
color. The LEDs will show their current state.

The payload will contain 4 bytes: START (0x1B), color ('R','Y','G'),
ID (1-3), and 1 byte XOR checksum. (Note: `0x1B` corresponds to ASCII
ESC.) You are not required to use the checksum. The starting beacons
will be located on the floor, pointing towards oncoming traffic.

The beacons use a 33 Ohm resistor (or three 100 ohm resistors --
brown-black-brown -- in parallel) which increases their intensity and
range to about 1.5 m. Beacon code will be provided
[Code](https://github.com/BU-EC444/04-Code-Examples/tree/master/ir-car-beacon-capture)


<p align="center">
<img src="/docs/images/ir-beacon.jpg" width="40%">
</p>
<p align="center">
<i>IR Starting Beacon/Stoplight</i>
</p>


