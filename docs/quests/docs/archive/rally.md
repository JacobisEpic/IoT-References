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
  - For steering and controlling car speed and direction
  - Logging of time elapsed from start, through each checkpoint, and to the finish 
  - Data are logged on a RPi-hosted database
  - Preset queries to the database result in a summary of checkpoint times for a run
  - Live streaming video coming from a webcam on the RPi on the buggy

- Buggy including
  - Range sensors for collision avoidance
  - PID control on set-point speed (forward direction, not required for reverse)
  - IR receiver to trigger start of race
  - Alpha display showing most recent split (time)
  - Decode QR code at checkpoints to get checkpoint number


## Running the course

We will set up a course in the classroom. A car will rest at a
starting line and will be triggered by an IR beacon signal. The car
will then be driven (via your remote control interface) to each
checkpoint, recording the elapsed time between checkpoints. The
checkpoint QR code will be read and saved with the elapsed time from
the previous checkpoint. This continues until the car returns to the
starting line and decodes the QR code found there.

After each transit, the most recent transit time should be displayed
on the alpha display.  The car must not hit any objects on the course
or the run will be disqualified. It will be helpful to design a preset
turning function to steer the car a fixed angle to the left or right,
to help overcome delays in communication that makes remote driving
difficult. This is intended to be used when turning is required, for example,
in the zone near the QR codes ("auto-turn zone").

<p align="center">
<img src="/docs/images/rally-course.jpg" width="70%">
</p>
<p align="center">
<i>Rally Course</i>
</p>

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work on Race Day
3. Reporting as per quest reporting instructions, but ***make your video of higher quality for sharing***


## Reference material
- Prior quests and skills
- [Rally (Wikipedia)](https://en.wikipedia.org/wiki/Rallying)

## Rubric  
| Objective criteria (0/1, 1=met)                                                                 | Rating | Max |
| ----------------------------------------------------------------------------------------------- | ------ | --- |
| Car is controlled through web interface with L, R, F, R, stop, and speed setpoint controls      |        | 1   |
| Video from car incorporated in single browser frame with driving controls                       |        | 1   |
| Client web interface to query for transit time history                                               |        | 1   |
| Car is driven remotely from URL and drives successfully including L, R, F, R, stop controls |        | 1   |
| Each QR code checkpoint is visited by car and decoded in program and logged                             |        | 1   |
| After collision stop, car can restart in reverse to reset                                                |        | 1   |
| Uses PID control for constant speed between checkpoints                                        |        | 1   |
| Starts course with either (a) IR green light signal from example IR transceiver, or (b) QR code flashed
on laptop from "R" to "G"|        | 1   |
| Range sensors are functional and prvent collisions; no collisions with any objects on course    |        | 1   |
| Displays most recent average transit time on alpha display                                          |        | 1   |
| Completes the course using remote control without nudges or touches                                   |        | 1   |


## Starting Signal for the Car 

- You can use the same [example
code](https://github.com/BU-EC444/04-Code-Examples/tree/main/ir-txrx-example)
from the IR-TXRX skill as a starting signal. A green 'G' sympbol from
the IR transmitter should trigger your car to start.

- Alternatively, you can use a QR code to start the car using a laptop
  display of two alternating codes: one with an encoded 'R' and the
  other with an encoded 'G'. Put this in a simple HTML page and
  display with a browser. You can hunt down a method to toggle the QR
  images in javascript or CSS. The QR codes are in a folder on git for
  the quests.