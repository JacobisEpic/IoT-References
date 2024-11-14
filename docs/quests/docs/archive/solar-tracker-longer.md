# Solar Tracker

In this quest you will create a system to track the sun for the
purpose of aligning a solar panel to realize the best orientation
based on time of day. The core parts of this have to do with keeping
time, controlling servo position, and reporting data on an
alphanumeric display.

<p align="center">
<img src="/docs/images/best-angle.jpg" width="50%" >
</p>

<p align="center">
Solar Model (https://www.mpptsolar.com)
</p>

## Description 

Two servos can be cascaded on different axes to realize angular
measurement in two dimensions. The first servo controls azimuth, or
the angle tranversed from East-West. This represents the position of
the sun relative to the earth's rotation. The second servo controls
altitude, which is the angle up from the horizontal when facing south
(where the sun is found in the Northern hemisphere).

Most solar installations use a fixed azumuth of 0 deg (points South)
and an altitude established by the latitude. The Boston latitude of
aproximately 42 in Boston indicates and altitude of (90-42) = 48
deg. Unfortunately this angle only happens on the summer solstice. If
we can dynamically tilt the panels we can get better efficiency due to
the time of year and time of day.

<p align="center">
<img src="/docs/images/solar.png" width="100%" >
</p>

<p align="center">
Solar Tracking System
</p>



Your task is to use a small solar cell to track the position of the
sun and establish the difference between the fixed angles and the
dynamic ones.  The differences in azimuth and altitude should be
reported on the numeric display (in degrees).

Establishing a measured position can be done by a search process
consisting of (1) initially turning the solar cell to the predicted
angles for a (latitude/longitude, time) and (2) rotating +/- on
each axis to find a maximum measured output voltage on each axis. The
difference between the measured angles and the fixed angles should be
reported to the alphanumeric display.

To simiplify testing (since the sun moves pretty slowly), we will use the following:
- Measurement frequency: once every 10s 
- Light source: LED from a smartphone 
- Measurement: using the provided solar cell, level-shifted with a resistor divider, and connected to an ADC channel of the micro.
- Prediction model: based on location (Boston @ 42 deg latitude) 

## Solution Requirements
- Must keep track of time (time of day, day of year with no time loss). Printing to console is fine
- Must find values of azimuth and altitude at maximal 'sun' intensity once per measurement period 
- Must use two servos
- Must display error values determined by difference in measurement-derived values and the fixed solar panel


## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Complete self-assessment rubric
5. Investigative question: What approach can you use to make setting the time and date not hard coded? Elaborate.

## References
- https://en.wikipedia.org/wiki/Solar_azimuth_angle
- https://gml.noaa.gov/grad/solcalc/
- Note that there are CAD models for mounting the servos in tandem. See the quest subfolder called "cad"


## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| 1. Keeps track of time |  |  1     | 
| 2. Measures input from solar cell |  |  1     | 
| 3. Finds azimuth and altitude at maximum intensity |  |  1     | 
| 4. Drives two servos to position of maximum intensity |  |  1     | 
| 5. Cyclic behavior at design frequency driven by clock (not delays) |  |  1     | 
| 6. Reports errors on display in degrees  |  |  1     | 


## Implementation


<p align="center">
<img src="/docs/images/solar-servo2.png" width="35%">
</p>

<p align="center">
Servo Linkage
</p>

