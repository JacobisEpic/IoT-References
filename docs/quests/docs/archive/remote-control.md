# Find the Beacons by Remote Control, Decode the Message, Escape the Course

This quest rolls up earlier quests. This is a race to find a set of
beacons hidden in a maze. Each beacon will send out a fragment of a
hidden message; once all of the messages are gathered, a secret
message is revealed. You will design your car to be remote controlled
from a location away from the course.

<p align="center">
<img src="/docs/images/remote-drive.png" width="100%" />
</p>
<p align="center">
<i> </i>
</p>



This quest requires the following

The car:
- You will use the Pi and webcam as a video streamer either fixed above the
course providing an overview, or attached to the car, providing first-person view. 
- You will locomote inside a search space by
 remote control and by accessing the pi/web camera on the car or near the course
- You must avoid collisions using mandatory front sensors
- When you find a beacon, you will capture the emitted code and deliver to your application for assembly into
a longer message.

The application
- The car must be controlled through a web browser; controls are up to you but should include forward, backward, left, right.
- The video stream must be integrated into the same browser frame
- As the beacon codes are collected they will be catenated into a secret message (a URL)

The beacons:
- The beacons will use the same platform as Quest 4 (Self-Driving Car) except that in addition to ID, a fragment in the format of a 10 character string will also be returned.
- The catenated strings will form a URL of length 40 characters similar to the following example below.

String "whizzer.bu.edu/team-quests/primary/test0" distributed to the beacons as:

Beacon |Fragment | Indicator LED
------------| ------------- | -------------
1    	|whizzer.bu| Red
2	    |.edu/team-| Blue
3	    |quests/pri| Green
4	    |mary/test0| OFF

***IMPORTANT:***

The start byte has been changed to `0x1B` instead of `0x0A` to avoid
confusion when printing as a character -- `0x0A` was a newline
character. `0x1B` corresponds to ASCII the ESC code. In
addition, beacons have been renumbered. Beacon 0 no longer exist and
the number and ID goes from 1 to 4.

Assumptions:
- We will provide the beacons with the test fragments. On demo day we will include the final "escape the course" fragments.


## Assignment
1. Design and build this system
2. Demonstrate your solution
3. Report, video as usual

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
