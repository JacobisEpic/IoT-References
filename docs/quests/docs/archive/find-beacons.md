# Find the Beacons, Decode the Message, Escape the Course

This quest rolls up earlier quests. This is a race to find a set of
beacons hidden in a maze. Each beacon will send out a fragment of a
hidden message; once all of the messages are gathered, a secret
message is revealed. You may design your car to be autonomous or
remote controlled.

<p align="center">
<img src="/images/escape-course.jpg" width="100%" />
</p>
<p align="center">
<i> Escape the Course?</i>
</p>


This quest requires the following

The car:
- You must avoid collsions using mandatory front sensors
- You will locomote inside a search space without getting stuck, operating in either an
autonomous or remote controlled way (backups and turns are ok)
- You will report to a central server (pi) a 'watchdog timer' every 15 sec. that you are
actively searching, and the progress -- how far your wheels have traveled
in the sum of your forward wheel rotation -- of your search.
- The car will detect and decode a beacon signal and deliver this via wifi to the server 

The server
- The server will use node.js and will receive data from your car via push. This includes the watchdog timer message and the beacon message.
- Once your pi has received each of the required beacon messages, it will be able to serve up the secret 
message (the messages will catenate into a URL)
- The server will host a page that will show a dashboard including
  - Progress as a graph vs. time (forward distance traveled vs time)
  - Beacons discovered
  - Partial message completed
  - Real time video stream from central camera on pi (we will provide)
  - [Optional] steering and speed controls for remote control

The beacons:
- Same as the fob beacons except that the code returned will be a char string that is part of a URL
- The catenated codes (strings) will consist of a URL of length 40 characters
similar to the following: 

Assumptions:
- We will provide the beacons


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
