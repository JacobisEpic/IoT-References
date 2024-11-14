# Traffic lights

The idea here is to enable a traffic light to serve as a central
controller that interacts with oncoming vehicles. When a car
approaches the light, it communicates with the light controller to change the
signal to green, if appropriate.

Using our gear, we will use a single ESP32 as light controller (two
ways with red, green, yellow), and multiple ESP32s as cars.

You will need to develop the logic. We recommend state machines for
the traffic light and each of the incoming cars.


<p align="center">
<img src="/docs/images/street-light.png" width="50%" />
</p>
<p align="center">
<i> Smart Traffic Light</i>
</p>

Suggestions
- Use ESPNOW which enables peer-to-peer messaging
- Define your message structure so that you can pass sufficient information and easily interpret the car light request
- How do you realize a state machine in program code?
- What defines a good solution? How to quanitfy?

## Assignment
1. Work through the use cases and operating scenarios and make sure you have identified the traffic light behavior. 
2. Develop a state based model for the traffic light
3. Develop a state model for a car (this will be replicated)
4. Build up the ESP32 with traffic lights (LEDs)
5. Build up multiple ESP32s as cars (at least 2)
6. Test and demo
7. Report


## Reference material
- [ESPNOW](https://github.com/espressif/esp-idf/tree/master/examples/wifi/espnow)
