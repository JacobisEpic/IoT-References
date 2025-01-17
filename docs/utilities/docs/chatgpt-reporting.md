# AI Use Reporting Guidelines

## The Rules...

1. You must indicate in your reports when you have used an AI to
produce a solution or fragment

2. The fragment should be cited (in code comments when it has been
produced by the AI (cite the tool)

3. You must provide the prompts used to generate the fragment in your report.

4. You are responsible for understanding the results that you adopt;
the expectation is that you can defend the solution and justify its
correctness

## Reporting template for the README.md file:


## AI Use

I used {chat.openai.com GPT-3.5} on {8/30/2023} with the following prompt:

***Prompt***

```
Act as: Node.js developer
Technology stack: node.js, nxpress.js, serial.io, canvasjs
Functionality: graphing
Mandatory Fields: temperature, pressure, device ID, time (seconds)
Optional fields: 
Task: create javascript and HTML code for live plotting temperature
and pressure versus time for each value of (temperature, pressure,
device ID, time) received from the serial port

```

***Code Attribution***

I have included a comment in my code for this assignment stating the following:

```
// This code block was generated by {name} using {chat.openai.com
GPT-3.5} on {8/30/2023}

```
