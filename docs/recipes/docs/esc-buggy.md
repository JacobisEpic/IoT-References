# Calibrating ESC and Steering Servo -- BUGGY

The ESC -- Electronic Speed Control -- is a device that operates
similar to a servo except that it is designed to control the speed of
a motor. Our ESC is a 'brushed' type unique to the motor that comes
with the crawler.

***NOTE: This page refers to the ESC with the Buggy***, not the crawler. 

Like a regular servo, it operates across a range of PWM values with a
low-limit, a high-limit, and a mid-point. These are typically mapped
to reverse, forward, and neutral, with increasing speed proportional
from the deviation from the mid-point.  This is exactly how the
Crawler ESC works (Forward / Neutral / Neutral).  But not all ESCs
operate this way.

The buggy ESC control mode is of the type "Forward / Brake / Reverse."  To
reverse, one needs to "double click" by bringing the PWM signal from
midpoint to below midpoint twice in succession.  Otherwise the the
first time below the midpoint "brakes" the motor -- it continues
spinning but does not reverse.  

In each case, the ESC needs to be 'calibrated' to the PWM mid-point. The buggy ESC relies on a single 
calibration point (different from the crawler). 

<p align="center">
<img src="/docs/images/esc.jpg" width="50%">
</p>
<p align="center">
<i>ESC </i>
</p>

## Calibration step (buggy)

Do a one-time calibration at the time of ESC turn-on with 3 seconds of PWM at the midpoint.

****From the manual***

     "Calibrate the throttle range: Turn on the ESC switch, set the
     throttle stick to the neutral point and then wait 3 seconds for
     the completion of throttle range self-calibration; Beep sound
     emits if the self-calibration is successfully passed, then the
     ESC is ready to run.

***Operating Modes***

     "The “Fwd / Br / Rev” is the default option for the
     ESC. Fwd=Forward, Br=Brake, Rev=Reverse. “Fwd / Br / Rev” mode
     indicates the vehicle can go forward, backward and brake. This
     mode uses “Double-click” method to make the vehicle reverse. When
     moving the throttle stick from the neutral zone to backward zone
     for the 1st time, the ESC begins to brake the motor and the motor
     slows down but still running, so the backward action is NOT
     performed immediately. When the throttle stick is moved to the
     backward zone again, if the motor speed slows down to zero
     (i.e. stopped), the backward action will happen. This
     “Double-click” method prevents mistakenly reversing action when
     the brake function is frequently used in steering.

***Interpretation of the manual***

The ESC drives forward normally with increasing PWM signal from the
midpoint.  When PWM is decreased from midpoint, the motor does not
immediately reverse. The PWM signal needs to return to midpoint and
then decreased a second time to enable reverse.


***Code Steps to Calibrate***

1. Power on the ESC/buggy power (it will beep)
2. Power on the ESP
3. The ESP should immediately set the PWM signal to the ESC to mid value ("neutral")
4. Hold this value for 3000 ms
5. The ESC will beep if the calibration is successful 
6. Now you can control the ESC, varying the signal within the range

For the buggy, the measured values generated by the receiver (that we
have disconnected and are not using) are:

- 50 Hz PWM frequency
- Neutral (midpoint) pulse width: 1.500 ms
- Forward direction maximum pulse width: 2.100 ms
- Breaking/reverse direction minimum: 0.900 ms

It is possible that other values can be used (we do not have exact
specs for the ESC device).

This is done using PWM. Example calibration code is provided
below. Note, we are using the `mcpwm_set_duty_in_us()` function over
the duty cycle percentage instant.

OLD SOLUTION -- OBSOLETE: 

``` c
void calibrateESC() {
  mcpwm_set_duty_in_us(MCPWM_UNIT_0, MCPWM_TIMER_0, MCPWM_OPR_B, 1500); // NEUTRAL signal in microseconds
  vTaskDelay(3100 / portTICK_RATE_MS); // Do for at least 3s, and leave in neutral state
}

```
NEW Solution (2023-11-02)

``` c
void calibrateESC() {
 ESP_ERROR_CHECK(mcpwm_comparator_set_compare_value(comparator, example_angle_to_compare(0)));
 vTaskDelay(pdMS_TO_TICKS(3100)); // Do for at least 3s, and leave in neutral state
}
```

You only need to run this once, but each time after the ESC has
been turned on. We strongly recommend that you experiment with the
wheels of your crawler off of the table. Use a block to raise the wheels.

<p align="center">
<img src="/docs/images/elevate.jpg" width="50%">
</p>
<p align="center">
<i>Wheels Up When Flashing or Testing Code</i>
</p>


We've found that it works best to:
1. Program your ESP over USB.
2. Switch power to the crawler (use a power brick for crawler)
3. Turn on crawler before you turn on the ESP

Finally... remember that the crawler and motors are mechanical
devices. As such, their position, speed, velocity, etc. conform to
physical laws.  The best way to actuate the speed control is
incrementally over a reasonable time interval. Not zero to full speed
in 1 us.


## Reference Material
- [PWM Brief](/docs/briefs/design-patterns/dp-pwm.md)
- [ESP example code for servos](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/mcpwm/mcpwm_servo_control)
- [ESP-IDF Motor Control with PWM](https://esp-idf.readthedocs.io/en/latest/api-reference/peripherals/mcpwm.html)
- [Buggy Product Description](https://www.nitrorcx.com/51c852-fireblue-24ghz.html)
- [Buggy Product User Manual](https://p11.secure.hostingprod.com/@hobbypartz.com/ssl/ibuyrc/manual/51C852.pdf)
- [Buggy ESC Product Description](https://www.hobbywingdirect.com/collections/quicrun-brushed-system)
- [Buggy ESC Product User Manual](https://www.hobbywing.com/products/enpdf/QuicRunWP1625-WP860-WP1060.pdf)

<p align="center">
<img src="/docs/images/receiver-wiring-buggy.jpg" width="50%">
</p>
<p align="center">
<i>Reference Photo of RC Receiver Connections to ESC and Servo</i>
</p>
