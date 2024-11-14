# RTOS TASKs -- Free RTOS

In this skill you will exercise the features of a real time OS (RTOS)
as realized by the ESP32 FreeRTOS instance.  It will be helpful to
refer to the [Design
Pattern](/docs/design-patterns/docs/dp-tasks.md) for tasks in
FreeRTOS.

One of the features of RTOS is the scheduling of tasks based on
priority, particularly as it relates to timing. In the problem below,
your tasks will operate at different time scales and will interchange
data in a producer-consumer way.

In our problem, the ***first task*** will reuse the code from the [GPIO
skill](/docs/skills/docs/gpio-drive-leds.md) to count up or down in binary
using LEDs (3 LEDS on a breadboard).

A ***second task*** will read the state of a pushbutton. If the button is
pushed, the direction of counting should be reversed.

A ***third task*** will display the direction of counting on the
blue LED ("up" or "down").

Communication can be done via global variables (we will deal with
mutual exclusion later).

<p align="center">
<img src="/docs/images/tasks-led.jpg" width="60%">
</p>
<p align="center">
<i>Hardware Configuration</i>
</p>

## Assignment
1. Design these three tasks (each task should be a separate FreeRTOS task)
   - Task A: [Count up in binary](/docs/skills/docs/gpio-drive-leds.md) every 1 second (RGBY LEDs with 330 Ohm resistors please)
   - Task B: A button press to toggle from counting up to counting down or vice-versa (needs a pull-up or pull-down resistor depending on how you wire it up). This task sets the 'direction' value
   - Task C: Read the current 'direction' value and set display to the blue LED as "up" or "down"
2. Identify how to signal between tasks (global variables) via 'direction'
3. Report as usual


## FAQ
- How do you get the program to switch between tasks? See the design pattern for tasks.
- What's the circuit for the push button switch? See below.

<p align="center">
<img src="/docs/images/push-button.jpg" width="30%">
</p>
<p align="center">
<i> Push Button Switch Schematic</i>
</p>

## Reference Material
<!-----
- [Interrupts for Buttons](/docs/design-patterns/docs/dp-interrupts.md)
But note that this example no longer uses interrupts to time between the activites (async or sync)
----->
- [Design Pattern for Tasks in FreeRTOS](/docs/design-patterns/docs/dp-tasks.md)
- [ESP IDF Free RTOS](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/system/freertos.html)
- [Free RTOS Tutorial](https://www.freertos.org/tutorial/)

