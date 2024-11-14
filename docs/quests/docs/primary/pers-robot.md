# Indoor Robot Assistant

We all know how successful and pervasive GPS (or GNSS) for enabling
outdoor positioning and navigation. Indoors is a different
story. Materials use in construction reflect and attenuate GPS signals
originating from satellites, makng GPS unrelable there. Alternatives
exist using a variety of modalities including RF, ultrasound, light,
and IR. Each has pros and cons, but a typical application for indoor
positioning will yield positional accuracy of about 1m. This is pretty
good to identify where you are in a building, but no so good for
fine-grain control as might be necessary in many applictions. We
consider one such application involving mobile robots that might
assist us in some task. Examples of this sort of thing have been realized
as "Follow me" suitcases or meal delivery (see below).

<p align="center">
<img src="/docs/images/follow4.jpg" width="60%">
</p>
<p align="center">
<i>Mobile Assistive Robots</i>
</p>

<!--- We currently have several types of wheeled vehicles as robots to
choose from. These include Crawler and Buggy versions of RC vehicles
and the purple cars or "covered wagons". The crawler has a large
platform which is great. The buggy is a little smaller but is really
intended for high-speed operation. These are two extremes. Neither
turns well in our test space, but they are options for this quest.
The purple car in some ways less glamorous but has a feature that it
can turn 'in place.' It is also a little flaky due to the motor
performance varying with battery charge. Each of these deficiencies is
typical of any robot.
--->

The quest will involve navgating through a path in an indoor space
while avoiding a second vehicle. Key features of successful navigation
are not to collide with walls, people, or other robots.  In the past,
this quest has relied on multiple sensors for range (also using RF,
ultrasonic, light, and IR), but primarily to prevent collisions. A
more systematic deployment of infrastructure of devices is required to
support in-room or room-to-room navigation. We will use a motion
capture (MoCap) system by Optitrack that uses IR with reflectors and
camera tracking.

<p align="center">
<img src="/docs/images/infra1.jpg" width="70%">
</p>
<p align="center">
<i>Infrastructure to Support Indoor Positioning of Robots</i>
</p>


You will need to pick your vehicle type: crawler or purple car. There
are pros and cons here. The crawler is burly and has a huge payload
and is cool looking. It uses servos for steering and an electronic
speed controller. The purple car uses two motors and is steered by
controlling the difference in rotational speed of the two motors. Its
advantage is the ability to turn in place whereas the crawler needs
forward motion to turn.

<p align="center">
<img src="/docs/images/robot-comps1.jpg" width="70%">
</p>
<p align="center">
<i>Robot Options and Components</i>
</p>

In our setup the Optitrack cameras (12) are dispersed at the
perimeter of the working space and provide very high positional
accuracy (< 1cm) of tracked objects (objects are tagged with
reflective dots). The Optitrack software (Motive) combines angle and
range information to determine (x,y,z) coordinates in the space. The
coordinates will be accessible from a node.js server on our
network. We are not using the UWB components in the quest.

<!---
The UWB component is realized by self-contained boards placed as
"anchor" points around the space. Position information is obtained by
a unit attached to the robot when it queries each of the anchors and
then computes position by multilateration.~~~

--->

Both the UWB system (approx. $40 per anchor point) and Optitrack
system (approx. $12k for single room) are available in room 208. We
will use the Optitrack tracking as a service provided on the local
network to which you will interface.

The robot part will be implemented using a either the 4-wheeled crawler or the "covered wagon"
labeled with and optical tag. The robot will be controlled
using the ESP32 and will include sensors for ranging (to prevent
collisions).

<p align="center">
<img src="/docs/images/hood-up-down.jpg" width="20%">
</p>
<p align="center">
<i>Purple Car as "Covered Wagon" with Optical Tags</i>
</p>


The whole system comes together with multiple robots, Optitrack parts,
and server all operating on the same network. Multiple robots will
exist on the course due to the assignment (which uses pairs of
devices) and because each team will be using the same assets
(indicated as "shared").


<p align="center">
<img src="/docs/images/robot-opti1.jpg" width="70%">
</p>
<p align="center">
<i>System Architecture and Details</i>
</p>



## The Quest

The quest focuses on successfuly moving your robot through a set of
waypoints, without collisions, using positional data from the
Optitrack and obstruction data from your range sensor. Here is a strategy:
1. Interface the ESP32 to the car electronics
   - Crawler: Bring up the sero control on the ESP (via recipe)
   - Crawler: Establish ESC calibration (via recipe)
   - Purple car: Bring up the H-bridge and motor PWM
2. Establish the use of selected sensors on the vehicle
   - Ranging (LIDAR, Ultrasonic, or IR) for forward collision avoidance
3. Interface your ESP32 to the indoor positioning system:
   - Interface the ESP32 to the Optitrack node.js (put tags on the crawler)
4. Create a way to display your position graphically, using the
positional data, including the waypoints indicated
5. Demonstrate the positioning statically
6. Now you should design your driving control
   - Accommodate timing limits of sensors (how frequently can you read and process a sensor's data?)
   - Accommodate actuator timing (e.g., how frequently can you change wheel angle?)
   - Set PID timing (dt -- cycle time) that uses the real-time positional information
   - Make sure the timing is consistent (e.g., with timers or interrupts)
   - Make sure to check for collisions as a priority activity
7. Test the driving with a single pair of waypoints
8. Design your software to drive your vehicle through the set of
waypoints. Test

Very important: test each subsystem as it is built – don’t wait for
a ‘big bang’ approach to developing your solution.

## Test Track Implementation

Two robots should be assembled and tested. The test track involves following a figure-8 path through
the field of view of the Optitrack system as shown below.

<p align="center">
<img src="/docs/images/2robots.jpg" width="70%">
</p>
<p align="center">
<i>Test Track for Quest </i>
</p>





## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions



## Reference Material
- [PWM Design Pattern](/docs/design-patterns/docs/dp-pwm.md)
- [PWM Design Pattern](/docs/design-patterns/docs/dp-pwm.md)
- [PID For Wall Tracking and Speed Control Design Pattern](/docs/design-patterns/docs/dp-pid.md)
- [Recipe for Wiring ESP32 to Crawler](/docs/recipes/docs/buggy-interfacing.md)
- [Recipe for Calibrating ESC and Steering Servo -- Buggy](/docs/recipes/docs/esc-crawler.md)

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Start and stop instructions issued wirelessly from phone, laptop or ESP |  |  1     | 
| Sensor to prevent collisions |  |  1     | 
| Links to Optitrack for position information |  |  1     | 
| Uses feedback control when driving between waypoints or on track within 20cm error bound |  |  1     | 
| Turns successfully at waypoints |  |  1     | 
| Successfully traverses all waypoints in one go, no hits or nudges |  |  1     | 
| No collisions |  |  1     | 
| Graphic display of progress in 2D |  |  1     | 
| Two robots run concurrently on same track |  |  1     | 
