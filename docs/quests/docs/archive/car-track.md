# Self-Driving Car

In this quest you will use your skills with range sensing and control to
enable your car to self drive around a course. This is illustrated below.

<p align="center">
<img src="/docs/images/driving.png" width="100%" />
</p>
<p align="center">
<i>Course Layout </i>
</p>

Your car will be evaluated on a test track with the objective of
navigating from a start point, through the course, and to an end
point without colliding with surfaces or objects along the way.


Strategies
- We recommend that you model the system with states involving straight driving
and turn driving. Transitions are defined by the proximity of the beacons.
- Navigation through the course is determined by a set of linked waypoints
- Driving is aided by proximity of track outer wall. You can detect this with
one or more range sensors.
- Some periodic sensing--actuation function will be required to make this work that integrates
existing code for sensing, DC motor control, and getting signals from the beacons.
- PID (recommended but not required) can be used to maintain a constant angle of the car with respect to the wall.
- One objective point will be earned for implementing at least one of
(PID, communication of current segment location to web, or use of wheel speed control)


## Dependent Skills
- PID Control
- IR TX-RX
- State Models
- Building your car
- Range sensor
- DC motor control


## Assignment
1. Design and build your car with appropriate sensors
2. Integrate existing work on sensors, Demonstrate on track
3. The usual reporting


## Optional
- Use PID in keeping a set-point on the car


## Beacons

We will use four beacons using the protocol used in the leader
election running at ~~600~~ 1200 Baud . These beacons are capable of
transmitting and receiving IR data; however, you will use them in this
quest as a simple beacon radiating their IDs.

There are indicator LEDs on each beacon representing their IDs. IDs
can be toggled using the push button, however, they each start with a
different ID.

The payload has been simplified to two bytes: START (0x0A) and ID (0-3).

Indicator Color    | ID
------------       | -------------
RED                | 0
BLUE               | 1
GREEN              | 2
OFF                | 3

*** Turning beacon code ***
+ [Code](https://github.com/BU-EC444/ec444-repo/tree/master/ir-car-beacon)


<p align="center">
<img src="/images/ir-beacon.jpg" width="80%" />
</p>
<p align="center">
<i>IR Beacons </i>
</p>


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

