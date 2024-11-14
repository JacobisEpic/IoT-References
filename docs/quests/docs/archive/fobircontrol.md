# Teaching a Car to Drive

Neural networks can be trained on the demonstrations of human drivers
to learn to follow lanes and avoid obstacles. Your goal in this quest
is to teach an autonomous vehicle to drive by imitating an driving
expert (imitation learning).

Emergecy, lock/unlock, reverses for parking spot. Key-based control. 

- Construct two fobs. One receives one transmits. 
- Click to start, stop when encounter a wall.
- Turn control with a different button. 

<p align="center">
<img src="/docs/images/e2e.png" width="90%" />
</p>
<p align="center">
<i> </i>
</p>



## Description 

The overall procedure
involves three steps: (a) collecting data from multiple sensors, e.g.,
LiDAR, IR, camera using an expert driver (b) training a simple neural
network that learns to predict the control signals, i.e., steer and
throttle, from the sensor input (c) testing the model ideally in a
long corridor or along a sidewalk next to a building.




## Assignment

1. Design and build your solution to enable an end-to-end autonomous driving task
2. Demonstrate your work in the testing scenarios


## Problem Decomposition

1. Establish the use of selected sensors on the vehicle, e.g., LiDAR, IR, camera
2. Collect data comprising of sensor input (on the ESP32) and remote
control signals, i.e., steer and throttle, in diverse scenarios, i.e.,
routes with a set of turns and curves.
3. Save the data into a CSV either by saving data from the console
into a CSV, or sending the data to Node via UDP and then saving as a
CSV.
4. Leverage the CSV to build a tf.data.Dataset (See the abalone.csv
file in
https://github.com/tensorflow/tfjs-examples/tree/master/abalone-node)
5. Train your neural network using TensorFlow.js. A simple training
example can be found here:
https://github.com/tensorflow/tfjs-examples/tree/master/abalone-node
(Note: Use Python2.7 when setting up TensorFlow.js)
6. Once the model is trained, send instructions to back to the ESP32
from Node via UDP to apply your trained model to the steering and
throttle of the car.
7. Deploy the model on the rPI or ESP32 using the reference tools
below.

NOTE: It's critical to always operate vehicle at low speeds/ introduce
safety breaks.

Optional: Design your own neural network to predict control signals
from sensor input. An end-to-end driving network architecture example
is shown in Figure 4: https://arxiv.org/pdf/1604.07316v1.pdf

## Reference Material

- [TensorFlow.js Installation](https://www.tensorflow.org/js/tutorials/setup)
- [More TensorFlow.js Examples](https://github.com/tensorflow/tfjs-examples)
- [Additional AI resources for ESP](https://github.com/espressif/esp-nn)
- [EloquentTinyML](https://github.com/eloquentarduino/EloquentTinyML)
- [TensorFlow Lite for Microcontrollers](https://www.tensorflow.org/lite/microcontrollers)
- [TensorFlow Lite for esp-idf](https://github.com/espressif/tflite-micro-esp-examples)

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Does A  |  |  1     | |
| Does B  |  |  1     | |
| Does C  |  |  1     | |
| Does D  |  |  1     | |
| Does E  |  |  1     | |
| Does F  |  |  1     | |
| Does G  |  |  1     | |
