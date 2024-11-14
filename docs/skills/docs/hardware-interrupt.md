# Realize a Hardware Interrupt

Interrupts are an excellent mechanism to interface to external events
that are time based (such as ticks from a wheel sensor) or are
sporadic such as motion triggers. Interrupts can be used to avoid idle
polling loops and can be used to wake up a micro that is in a
low-power sleeping mode. Most micros have hardware to produce
time-based interrupts which are also useful for establishing
sleep/wake duty cycling as a means to achieve low power,
battery-conserving operation.  Smart phones make extensive use of such
techniques to extend battery range.  We will employ these techniques for
our micro as well.

The basic idea for hardware interrupt is to trigger the micro to stop
the current execution, push program state onto the stack, and vector
to a specific memory address to service the interrupt. The behavior of
the service is specified in your program. There are some other details
about disabling interrupts during the service routine, dealing with
multiple priority levels, and preventing race conditions, but the
concept is very effective in embedded systems.

<p align="center">
<img src="/docs/images/button-int.jpg" width="60%">
</p>
<p align="center">
<i>Hardware Configuration</i>
</p>



## Assignment/Requirements

Your task is to implement two programs: (a) one with a polling loop
and (b) one with interrupts.

1. Wire up the pushbutton switch on one of the GPIO pins that supports interrupts
2. Wire up the four LEDs with 220 Ohm or 330 Ohm resistors
3. Your program should act as follows:  when the button is pressed, the LED should toggle through the LEDs, one lit at a time per button push.
4. Write and demonstrate two programs specified by
    - Onw program polls the state of the button push
    - The second program is interrupted to service the button push, then returns to the main program
6. Report out your code, results, pics etc.


## Reference material
- [Design Pattern for Polling](/docs/design-patterns/docs/dp-polling.md)
- [Design Pattern for Interrupts](/docs/design-patterns/docs/dp-interrupts.md)
- [Timer Group Interrupts](https://github.com/espressif/esp-idf/tree/17ac4bad7381e579e5a7775755cc25480da47d97/examples/peripherals/timer_group)
- [ESP32: Interrupt Allocation](https://esp-idf.readthedocs.io/en/latest/api-reference/system/intr_alloc.html)
- [ESP32: Pulse Counter Interrupts](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/pcnt.html?highlight=hardware%20interrupts#pcnt-api-using-interrupts)
- [ESP IDF GPIO Interrupt Example](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/gpio/generic_gpio)
- [EC444 Example](https://github.com/BU-EC444/04-Code-Examples/tree/main/button-timer)
