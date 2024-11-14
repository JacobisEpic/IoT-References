# Trilateration

Trilateration, not to be confused with Triangulation, uses a set of
three ranges to determine the location of a point in two dimensional
space. The general case is called multilateration, which has the
potential to improve on the accuracy of trilateration.

Whaaat?  This is about indoor positioning. We will get signal strength
from multiple RF beacons, and using the estimated distances, we do
some math to find our x,y coordinates.

<p align="center">
<img src="/docs/images/trilat.png" width="80%">
</p>
<p align="center">
<i> Operating Scenario for Positioning</i>
</p>

We're using WiFi so beacons are the WiFi and are RF sources. Your job
is to use the ESP32 and measure signal strengh from each SSID,
estimate ranges, then do the math, and voila, an x,y position
estimate.

Here is what you need:

- Three APs with known locations
- Need a function to ping the APs and return signal strength
- Need a relationship between signal strength and range
- Implement trilateration math on the ESP32 (see example code)
- Return position estimate


## Assignment
1. Set up as above, use your ESP32 to report position on your laptop by console or by alpha display
2. Demo
3. Report

## Reference material
- [Trilateration](https://en.wikipedia.org/wiki/Trilateration)
