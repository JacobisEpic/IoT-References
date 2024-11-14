# Sharp IR Range Sensor

Here we are using the Sharp IR Range Sensor. This uses an IR
source to reflect off of an object to measure distance at a receiver
mounted on the same unit. We have two types of this device, a short-range version (10 cm--80 cm) and
a long-range version (10cm--120cm). Check your part number. 

<p align="center">
<img src="/docs/images/IRrangefinder.jpg" width="10%">
</p>
<p align="center">
<i> IR Range Finder</i>

Notes on the Sharp rangefinder
- Accepts Vcc of 4.5 to 5.5V
- Range of 10 cm -- 80 cm or 10 cm -- 150 cm, depending on version
- Senses approx. every 40 ms with analog out
- Analog output does not exceed 3.3V; you do not need a voltage divider (even though Vcc is 5V)
- Sensitive to voltage supply changes, use capacitor on Vcc if possible

<p align="center">
<img src="/docs/images/IR-range-concept.png" width="70%">
</p>
<p align="center">
<i> IR Range Concept </i>
</p>

We recommend:
- ADC input
- NOTE: you will need to set the ADC attenuation factor [ADC Guide](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/adc.html)
- Operates best at range: need to collect data and curve fit, possibly
  linear approximation of voltage to range except at close range.
- Use a capacitor on Vcc if you have one



## Assignment
1. Look up the specs of the IR sensor and design an appropriate way to connect to the ESP32 ADC. Must be scaled
2. Wire it up
3. Write the code to read from the device, convert to engineering units, and display the results on the console, sampled every 2 s.
4. Write up results, pics, and the usual


## Reference Material
- [Sharp Long Range IR Rangefinder](https://www.sparkfun.com/datasheets/Sensors/Infrared/gp2y0a02yk_e.pdf)
- [Sharp IR Rangefinder](https://www.sparkfun.com/products/242)
- [ESP32 ADC Control](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/adc.html)
- [ESP-IDF Example Code](https://github.com/espressif/esp-idf/tree/39f090a4f1dee4e325f8109d880bf3627034d839/examples/peripherals/adc)


<p align="center">
<img src="/docs/images/IR-range-wiring-new.png" width="70%">
</p>
<p align="center">
<i> IR Range Finder Wiring</i>
</p>