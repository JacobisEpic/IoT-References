# Pulse Width Modulation (PWM)

PWM is a simple modulation protocol typically used in servo control
and also intensity control of LEDs. Compared to analog control, PWM is
useful in that values are either high or low, which is easier to
design as it does not require digital-to-analog (DAC) converters. Here
are some key takeaways as it pertains to the ESP32 and the MCPWM
peripheral.

## Frequency
Changing frequency will affect the period of a complete cycle. f1 has
a higher frequency but a shorter period than f2.

<p align="center">
<img src="/docs/images/pulses-freq.png" width="50%">
</p>
<p align="center">
<i>Changing PWM Frequency With Constant Duty Cycle</i>
</p>

## Pulse Width

With pulse width control, you change the width of the pulse but not the frequency.

The ESP32 MCPWM peripheral allows you to explicitly change your pulse
width. This affects the pulse width in the time domain and is self
explanatory. Interesting to note is that dependent on your frequency,
your signal will look different **but with the same pulse
width**. Frequency is of less significance in servo control just as
long as the max pulse width fits within the period defined by
frequency. Servo control is typically defined using pulse width.

Both signals have the same pulse width but different frequencies.

<p align="center">
<img src="/docs/images/pulse-width.png" width="50%">
</p>
<p align="center">
<i>Changing the Frequency with Constant Pulse Width</i>
</p>

## Duty Cycle

Sometimes it is also useful to vary the duty cycle of your signal from
0 to 100 percent. This is useful for something like LED intensity
control, where the interest is in some percentage of brightness at a
fixed frequency. Dimming is a result of average intensity over time.

These are the same signals as above, but they represent different duty
cycles as a result of different frequencies.

<p align="center">
<img src="/docs/images/duty-cycle.png" width="50%">
</p>
<p align="center">
<i>Different Duty Cycles with Different Frequencies</i>
</p>

Here duty cycle is fixed with different frequencies and as a result
pulse width is different.

<p align="center">
<img src="/docs/images/duty-cycle-fixed.png" width="50%">
</p>
<p align="center">
<i>Changing Frequencies with Constant Duty Cycle</i>
</p>

## Code for PWM on the ESP32

As with other code, the PWM control on the ESP32 has evolved over the
years. The hardware device is called the MCPWM (Motor Control PWM)
unit. There are multiple independent "timer groups" that can be used
to generate signals. We only need one output for our servo control,
but will use a second one for speed control of the buggy. The MCPWM is
way complicated to be able to support a wide variety of modulation
types. Our use is relatively straighforward, but we need to deal with
(program) the myriad control options.

The major components of the MCPWM that are relevant to us are (from the ESP-IDF Guide):

- MCPWM Timer: The time base of the final PWM signal
- MCPWM Operator: The module that is responsible for generating
  the PWM waveforms. It consists of other submodules including comparator and
  PWM generator
- MCPWM Comparator: The compare module takes the time-base count value
  as input, and continuously compares it to the threshold value
  configured. When the timer is equal to any of the threshold values,
  a compare event will be generated and the MCPWM generator can update
  its level accordingly.
- MCPWM Generator: One MCPWM generator can generate a pair of PWM
  waves, complementarily or independently, based on various events
  triggered by other submodules like MCPWM Timer and MCPWM Comparator.

The aforementioned units correspond to API calls in the code.

The [ESP example
code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/mcpwm/)
is an excellent starting point for a single conventional servo. You
can have a look at the course example code (which is the same but with
more detail in the comments). As with other units, the [ESP-IDF
Programming Guide MCPWM
Unit](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/mcpwm.html)
reveals the details of the APIs.

Here are snippets from the example code explaining the setup. First
the servo parameter defines which are updated when the servo specs are
different (for example, with the buggy speed control).

``` c
// These are typical servo parameters to configure the pulse width range and setpoints
#define SERVO_MIN_PULSEWIDTH_US 500   // Minimum pulse width in microseconds
#define SERVO_MAX_PULSEWIDTH_US 2500  // Maximum pulse width in microseconds
#define SERVO_MIN_DEGREE        -90   // Minimum angle
#define SERVO_MAX_DEGREE        90    // Maximum angle

#define SERVO_PULSE_GPIO             0        // GPIO connects to the PWM signal line
#define SERVO_TIMEBASE_RESOLUTION_HZ 1000000  // 1MHz, 1us per tick
#define SERVO_TIMEBASE_PERIOD        20000    // 20000 ticks, 20ms (this corresponds to 50Hz)
```

Now the MCPWM configuration (some logging steps removed, but shows the major calls)

``` c
    mcpwm_timer_handle_t timer = NULL;               // Create PWM timer
    mcpwm_timer_config_t timer_config = {            // Configure PWM timer 
      .group_id = 0,                                 // Pick PWM group 0
      .clk_src = MCPWM_TIMER_CLK_SRC_DEFAULT,        // Default clock source 
      .resolution_hz = SERVO_TIMEBASE_RESOLUTION_HZ, // Hz
      .period_ticks = SERVO_TIMEBASE_PERIOD,         // Set servo period (50 Hz for example)
      .count_mode = MCPWM_TIMER_COUNT_MODE_UP,       // Count up
    };
    ESP_ERROR_CHECK(mcpwm_new_timer(&timer_config, &timer));

    mcpwm_oper_handle_t oper = NULL;                 // Create PWM operator 
    mcpwm_operator_config_t operator_config = {      // Configure PWM operator
      .group_id = 0,                                 // operator same group and PWM timer
    };
    ESP_ERROR_CHECK(mcpwm_operator_connect_timer(oper, timer)); // Connect PWM timer and PWM operator

    mcpwm_cmpr_handle_t comparator = NULL;           // Create PWM comparator from PWM operator
    mcpwm_comparator_config_t comparator_config = {
        .flags.update_cmp_on_tez = true,             // Updates when timer = zero
    };
    ESP_ERROR_CHECK(mcpwm_new_comparator(oper, &comparator_config, &comparator));

    mcpwm_gen_handle_t generator = NULL;             // Create generator
    mcpwm_generator_config_t generator_config = {    
        .gen_gpio_num = SERVO_PULSE_GPIO,            // Output to GPIO pin 
    };
    ESP_ERROR_CHECK(mcpwm_new_generator(oper, &generator_config, &generator));

    // set the initial compare value, so that the servo will spin to the center position
    ESP_ERROR_CHECK(mcpwm_comparator_set_compare_value(comparator, example_angle_to_compare(0)));

    // go high on counter empty
    ESP_ERROR_CHECK(mcpwm_generator_set_action_on_timer_event(generator,
        MCPWM_GEN_TIMER_EVENT_ACTION(MCPWM_TIMER_DIRECTION_UP, MCPWM_TIMER_EVENT_EMPTY, MCPWM_GEN_ACTION_HIGH)));

    // go low on compare threshold
    ESP_ERROR_CHECK(mcpwm_generator_set_action_on_compare_event(generator,
        MCPWM_GEN_COMPARE_EVENT_ACTION(MCPWM_TIMER_DIRECTION_UP, comparator, MCPWM_GEN_ACTION_LOW)));

    ESP_ERROR_CHECK(mcpwm_timer_enable(timer));       // Enable timer
    ESP_ERROR_CHECK(mcpwm_timer_start_stop(timer, MCPWM_TIMER_START_NO_STOP)); // Start and run continuously
```
Then the operational part

``` c
    // This code drives the servo over a range
    // The PWM is changed slowly allow the (mechanical) servo to keep up 

    int angle = 0; // Initial angle
    int step = 2;  // Step size
    while (1) {
        ESP_LOGI(TAG, "Angle of rotation: %d", angle);
        ESP_ERROR_CHECK(mcpwm_comparator_set_compare_value(comparator, example_angle_to_compare(angle)));
        // Add delay, since it takes time for servo to rotate, usually 200ms/60degree rotation under 5V power supply
        vTaskDelay(pdMS_TO_TICKS(500));
        if ((angle + step) > 60 || (angle + step) < -60) {
            step *= -1;
        }
        angle += step;
    }
```

## Reference Material
- [ESP-IDF Example Servo Code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/mcpwm/)
- [Example Servo Code with additional comments](https://github.com/BU-EC444/04-Code-Examples/tree/main/servo)
- [ESP-IDF MCPWM](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
