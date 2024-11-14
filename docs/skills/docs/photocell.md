# Measuring Light with a Photocell (or Solar Cell)

We have two parts in the kit that are useful for measuring light
intensity. These are a photocell and a solar cell. They operate on
different principles. The photocell generats a variable resistance
suitable for quantifying signal using a voltage divider. The solar
cell, in contrast, produces a current and voltage based on its load
and the incident light.

The photocell is easier to use but has a limited range. It is mostly
used for things like detecting ambient light in order to set the
intensity levels of displays or to turn out security lights. 


<p align="center">
<img src="/docs/images/photocell-monitor.jpg" width="50%">
</p>
<p align="center">
<i>Photocell Signal Measurement</i>
</p>

<p align="center">
<img src="/docs/images/solar-monitor.jpg" width="50%">
</p>
<p align="center">
<i>Solar Cell Signal Measurement</i>
</p>

## Assignment
1. Choose an appropriate resistor for the voltage divider circuit for your photocell.
2. Wire it up on an ADC input
3. Write the code to read from the ADC, convert to engineering units, and display the results on the console, sampled every 2 s.
4. Write up results, pics, and the usual


## Reference Material
- [ESP32 ADC Example Code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/adc/oneshot_read)
