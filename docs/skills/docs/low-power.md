# Quantify Energy Use in Different Operating States

Low power consumption is essential in most connected devices,
especially when operated on batteries, but also when used at
scale. For example, without a low-power operating mode, adding a micro
in every light bulb would be prohibitively costly from an energy
standpoint. Even when the bulbs are 'off.'

In this exercise, you will quantify the energy consumption of the ESP32 in each of the operating states.

## Assignment/Specification
- Research the operating states for the device in the device guide
- Write a program that cycles the states of the device, 10s for each mode
- Using the analog discovery board, establish the operating current in each mode (how?)
- Record data, write up, discuss results


## Reference material
- [ESP32: Power Management](https://esp-idf.readthedocs.io/en/latest/api-reference/system/power_management.html)
- [ESP32: Ultra Low Power Coprocessor](https://esp-idf.readthedocs.io/en/latest/api-guides/ulp.html)
