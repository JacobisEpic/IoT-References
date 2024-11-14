# Battery Voltage Monitor

In this exercise you will measure a voltage on your board at an ADC
pin and display on the console.  Normally this would be a
battery voltage, but as a precaution, we will set up a divider on the
board's 3V output so that there is no chance that you will exceed the
input voltage of the ADC.

<p align="center">
<img src="/docs/images/vom.png" width="80%">
</p>
<p align="center">
<i>Alpha Display to Report Battery Voltage</i>
</p>

Normally there are two considerations here (1) making sure the voltage
divider drops the voltage down to somthing within the limits of the
ADC (e.g., 3.3V) and (2) setting the scale ("attenuation") in your ADC
configuration so that the ADC *spans* the righ range of
measurement. For example, a medical thermometer spans a range of 34C
to 38C whereas an outdoor thermometer might span -20C to 45C. These
have different ranges and different maximum values.

You will need to setup an ADC channel with a suitable voltage divider
to produce less than 3.3V. Then you need to work with the attenuation
factors to get it in range. Plan to program your ADC to read every
100ms, average the results over 1s and then display on the alpha
display send to the console. The input to your divider (not your ADC
pin) should be the 3V voltage pin of the Huzzah board.

If you have a capacitor handy, you can connect this between the input
of the ADC and GND to reduce noise on the input signal.

## Assignment
1. Wire it up
2. Code it up
3. Demonstrate and report

## Reference Material
- [ESP-IDF Example Code](https://github.com/espressif/esp-idf/tree/39f090a4f1dee4e325f8109d880bf3627034d839/examples/peripherals/adc)
- [Huzzah Power Options](/docs/utilities/docs/powering-esp.md)
- [ESP32 ADC Guide](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/adc_continuous.html)
