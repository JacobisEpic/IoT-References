# Pseudo-Mechanical Clock

Our micro is more than capable of realizing an electronic watch or
alarm clock function. It's probably more powerful than most wrist-worn
smart watches.  In this quest you will wrangle the features of the
ESP32 to build a simple alarm clock. But we'll make it more
interesting by adding mechanical clock hands to indicating passing time. How you define time on the hands
is up to you to decide. 

<p align="center">
<img src="/docs/images/quest1.png" width="50%" />
</p>
<p align="center">
<i> Pseudo-Mechanical Clock</i>
</p>

## Assignment
1. Design the functions of your alarm clock and how you
plan to deliver the current time, the alarm signal, and the user
control. Use the provided alphanumeric display (I2C based).
2. Agree on target performance as assessment criteria (e.g., reports
time every second). Be complete, but keep it simple and objective.
3. Incorporate two servos to indicate passing minutes and seconds. For
example, divide the servo arm range by 60 to define the increments for
seconds or minutes. Each arm sweeps a scale of range 0-60.
4. Build your solution and demonstrate
5. Write up a description of how you built your device. Include
concepts, modules, APIs, tools, etc.
6. Submit a < 90s video of your report. Everyone must be on the video.
7. Bonus: connect to ntp.org to glean global time


## Notes
- You can use the alphanumeric display skill or the LED dot matrix skill in this solution
- Stepper or servo are each reasonable as well

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
