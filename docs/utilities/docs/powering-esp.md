# Powering the ESP32

Tips on powering the ESP32 (Adafruit Feather edition) and available output supplies.

<p align="center">
<img src="/docs/images/esp-power.jpg" width="100%"> 
</p>
<p align="center">
<i>From Adafruit</i>
</p>

The ESP32 runs on 3.3V and uses 3.3V logic. The [Adafruit ESP32
Feather guide](https://learn.adafruit.com/adafruit-huzzah32-esp32-feather/power-management)
provides ample information. Consolidated:

- Micro USB from constant 5V source
  - 5V regulated to 3.3V
  - USB can be plugged into battery pack, AC to DC USB adapter, laptop

- Lithium Polymer battery (4.2/3.7V) with JST
  - Regulated to 3.3V
  - Battery will also charge with built-in charger at 200mA if USB plugged in

- `USB` pin
  - Access to 5V when USB plugged in
  - Can also provide ***regulated*** 5V when USB is not plugged in. An example would be the 5V output from the crawler ESC (later quest)

- `BAT` pin:
  - Mostly for accessing LiPo battery output
  - **Do not use alkaline or NiMH batteries on `BAT` as it will destroy the charger**
  - **Do not use RC batteries on `BAT` as it will destroy the board!**

- `3V` pin:
  - Output of the 3.3V regulator
  - Powers the ESP32
  - Can power low-power peripherals (<500mA)
  - `EN` pin turns off the regulator and also power to the ESP32
