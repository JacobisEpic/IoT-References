# The Thermistor

Measuring temperature is a pretty common thing. It's part of the
weather report and for telling you how hot to cook a pizza, but it's
also critical for many control systems like HVAC, 3D printer nozzle
temp control, automotive engine performance optimization, etc. There
are different types of thermometers of course. We will use the
inexpensive variable resistance type.

There are two devices provided in the kit. One is a cheap thermistor
on bare wire leads. It's pretty good on the breadboard for measuring
ambient temp. The other device is 'waterproof' and is packaged as a
probe on wires.  To use either device you need to create a voltage
divider circuit that feeds into the ESP32 ADC. Be mindful of the range
and voltage limits on the ADC when you design the circuit. Remember
Ohm's law and voltage divider math please.

Also consider that the variable resistor generates a resistance as a
function of temperature and with a fixed input voltage and an output
voltage as a function of temperature. Your job includes converting this
to an output in engineering units with appropriate baseline (e.g., 0
deg C).

<p align="center">
<img src="/docs/images/thermcheap.jpg" width="27.3%"><img src="/docs/images/thermistor.jpg" width="50%">
</p>
<p align="center">
<i>Thermistors -- bare wire and encapsulated</i>
</p>

## Assignment
1. Choose an appropriate resistor for the voltage divider circuit for your
thermistor.
2. Wire it up on an ADC input
3. Write the code to read from the ADC, convert to engineering units, and display the results on the console, sampled every 2 s.
4. Write up results, pics, and the usual


<p align="center">
<img src="/docs/images/thermdivider.jpg" width="25%">
</p>
<p align="center">
<i>Thermistor Voltage Divider</i>
</p>


## FAQ
1. The ADC reading seems to be constant.
Answer: Make sure to set the ADC scaling factor. You are probably operating at an input voltage which is out of range. 


## Reference Material
- [ESP32 ADC Example Code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/adc/oneshot_read)
- Thermistor: NTC mf52-103; 10K Ohm, B value: 3435 (+/- 1 percent)
- Temp Probe: XLX-1516 (you can assume similar values to the thermistor)
- [Thermistor Datasheet](https://www.eaa.net.au/PDF/Hitech/MF52type.pdf)
- [Thermistor Use Guide](https://learn.adafruit.com/thermistor/using-a-thermistor)
- [Thermistor Parameters Explanation](https://www.jameco.com/Jameco/workshop/TechTip/temperature-measurement-ntc-thermistors.html)
