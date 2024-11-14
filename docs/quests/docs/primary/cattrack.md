# Smart Cat Collar

This quest is to build an instance of a wearable device that records
biometrics and reports back to a central graphical hub. This year
we're going to focus on cats and their weird behavior.

Our cat's acitvity mostly consists of alternating between sleeping and
parkour with occasional bio breaks. The goal of this quest is to use
an accelerometer to establish the activity and report this in a
graphical format in modes of ('Highly Active,' 'Active,' and
'Inactive'). We also want a function on the device to display the
cat's name (Otto) and most recent activity classification.

<p align="center">
<img src="/docs/images/catcollar.jpg" width="100%">
</p>
<p align="center">
<i>Cat Track -- Smart Cat Collar</i>
</p>

The key features of the collar are:
- Keeps track of time of day in hour, min, sec
- Provides a button to trigger display of name and current activity and time in activity 
- Measures cumulative duration of activies in three states 
- Reports data to laptop for display as stripchart in real time (time, temperature, activity type)

This quest is about using the I2C bus, the alphanumeric
display, and accelerometer, and graphics output.

## Assignment
1. Design and build your solution to meet criteria specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions

Plan to wire up the buzzer because it will be used in the next quest. 

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Corectly keeps track of time |  |  1     | 
| Measures acceleration |  |  1     | |
| Provides reasonable classification of acceleration |  |  1     | |
| Provides continuous reporting of time, temperature, and activity to laptop |  |  1     | 
| Alphanumeric display triggered by button press |  |  1     | 
| Alphanumeric display shows cat name and current activity and time in activity |  |  1     | 
| Data at laptop plotted as stripcharts |  |  1     | 

Please state any assumptions made in producing the outputs (display values or stripcharts). 

## Reference material
- [Serial Port Module](https://www.npmjs.com/package/serialport)
- [Serial to Node Without a File Example](https://github.com/BU-EC444/04-Code-Examples/tree/main/serial-esp-to-node-serialport)