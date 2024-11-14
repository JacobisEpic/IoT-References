# Online Appliance

There are many possible IoT appliances. We thought of a smart toaster,
smart rice cooker, smart coffee maker, etc. etc. But we couldn't
decide on one type, so we abstracted the qualities of any smart thingamajig.

The key features of a smart appliance are going to be:
- Does something in your home, possibly while you are away (needs a scheduler like the one in our clock quest)
- Control and monitor it remotely (needs sensors, camera, actuators, network access, IP protocols)
- Turns high power things on and off -- "cooking" (needs to interface to smart plug)
- Programmable locally, or remotely

A typical use case would be: I connect to my device from work, control
an actuator (servo) to put coffee into the hopper, set a time to turn
on the brewing. The brewing starts at some programmed time, the
brewing stops.  If I check on status I will get a report on the state
of the machine and a web stream of the brew.

<p align="center">
<img src="/docs/images/toaster.png" width="100%" />
</p>
<p align="center">
<i>Smart Appliance Scenario </i>
</p>

## Strategy 

As with all of these assignments, there are a lot of moving parts, but
each part is not as complex as it sounds. We approach this problem
with the following breakdown:

- Get the ESP32 to talk to a WiFi access point to establsh connectivity
- Establish how you will transfer data from the ESP32 to a web client or server
- Design the web client (page) to provide control (buttons, display of video)
- Adopt servo control from prior exercise
- Integrate all together

- We are advocating having the ESP32 to send data to your client or
  server located on your laptop, but there are certainly different
  ways of doing this.

## Assignment
1. Decide what kind of appliance you want to model and determine it's
behavior. You can pick any one in the illustration. Define the
behavior of the device as a state diagram (some aspect of the system)
2. List controls -- local and remote -- and how you want to be able to
access and control them. Data will need to be sent to and from the
device across the internet.
3. Include a local alphanumeric display
4. Include a remote user interface to control the device
5. Maintain state somewhere in the system -- best if on the device
6. Include a local web cam (on the RPi), a thermistor, PWM control of a servo, a power control switch
7. Include any time scheduling aspects of the device
8. Program your design on the device with hooks for remote control via HTTP
9. Agree on target performance as assessment criteria (e.g., reports
time every second). Be complete, but keep it simple and objective.
10. Demonstrate your solution
11. Write up a description of how you built your solution. Include
concepts, modules, APIs, tools, etc.
12. Submit a < 90s video of your report. Everyone must be on the video.
13 Optional: in addition to your solution, implement using IFTTT


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
