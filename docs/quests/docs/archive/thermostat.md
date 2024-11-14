# Remote Control Thermostat

It's old news, but NEST was started by some former Apple employees who
built a company based on a thermostat product.  NEST was sold to
Google for more than 3 billion dollars. Their product has some cleaver
features, but we can build most of the functionality with parts in our
kit.

One thing that NEST figured out is the difference between the device
and the overall application. This will be reflected in (a) building
your wireless thermostat and (b) providing value in how the data are
collected, processed, and consumed by humans.

<p align="center">
<img src="/docs/images/nest.jpg" width="20%" />
</p>
<p align="center">
<i> NEST?</i>
</p>

## Assignment
1. Design a micro-based wireless thermostat. Wire it up. Plan to produce regular measurements of temperature in engineering units. You can use either sensor type provided in the kit.
2. Wire up at least 4 identical units.
3. Program your device to measure and record temperature every 10s. Data should be send wirelessly to a host for recording, capturing the time, temperature, device ID, and any other relevant data.
4. Use the Rpi as web host (you can prototype on your laptop). Data should be saved on the host in either (a) flat txt file, (b) JSON, (c) database tables
5. Serve up the data based on query (ideally with DBMS program, but not an absolution requirement)
6. Use node.js and chart.js to create standard queries to the data based on (a) real time strip chart and (b) historical time window.
7. Agree on target performance as assessment criteria. Be complete, but keep it simple and objective.
6. Demonstrate your solution
7. Write up a description of how you built your solution. Include
concepts, modules, APIs, tools, etc.
8. Submit a < 90s video of your report. Everyone must be on the video.


## Reference material
- [NEST products](https://nest.com)
- [Echobee products](https://www.ecobee.com)

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
