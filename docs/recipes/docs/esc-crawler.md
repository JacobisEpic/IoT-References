# ESC -- Crawler

The ESC -- Electronic Speed Control -- is a device that operates
similar to a servo except that it is designed to control the speed of
a motor. Our ESC is a 'brushed' type unique to the motor that comes
with the crawler.

<p align="center">
<img src="/docs/images/esc.jpg" width="50%">
</p>
<p align="center">
<i ESC </i>
</p>

Like a regular servo, it has three positions: left, right, and
neutral; except that these are mapped to backwards, forwards, and
neutral.

Also different, the ESC needs to be calibrated once at start up: you need
to tell the ESC what are the min, max, and neutral values.  Here is
how to do it:

1. Power on the ESC
2. Set PWM to high value // full forwards
3. Wait 1000 ms
4. Set PWM to low value // full backwards
5. Wait 1000 ms
6. Set PWM to mid value // neutral
7. Wait 1000 ms
8. Leave PWM at mid value

Under this scheme, you need to decide the high, low, and neutral PWM
values. We suggest:

- Low: 0.700 ms
- High: 2.100 ms
- Neutral: 1.400 ms

But other values can be used.  

This is done using PWM. Example calibration code is provided below. Note, we are using the `mcpwm_set_duty_in_us()` function over the duty cycle percentage instant.

``` c
void calibrateESC() {
  vTaskDelay(3000 / portTICK_RATE_MS);  // Give yourself time to turn on crawler
  mcpwm_set_duty_in_us(MCPWM_UNIT_0, MCPWM_TIMER_0, MCPWM_OPR_B, 2100); // HIGH signal in microseconds
  vTaskDelay(1000 / portTICK_RATED_MS);
  mcpwm_set_duty_in_us(MCPWM_UNIT_0, MCPWM_TIMER_0, MCPWM_OPR_B, 700);  // LOW signal in microseconds
  vTaskDelay(1000 / portTICK_RATE_MS);
  mcpwm_set_duty_in_us(MCPWM_UNIT_0, MCPWM_TIMER_0, MCPWM_OPR_B, 1400); // NEUTRAL signal in microseconds
  vTaskDelay(1000 / portTICK_RATE_MS);
  mcpwm_set_duty_in_us(MCPWM_UNIT_0, MCPWM_TIMER_0, MCPWM_OPR_B, 1400); // reset the ESC to neutral (non-moving) value
}

```

You only need to run this once, but each time after the ESC has
been turned on. We strongly recommend that you experiment with the
wheels of your crawler off of the table.

We've found that it works best to:
1. Program your ESP over USB.
2. Switch power to the crawler
3. Turn on crawler and ESP simultaneously

Finally... remember that the crawler and motors are mechanical
devices. As such, their position, speed, velocity, etc. conform to
physical laws.  The best way to actuate the speed control is
incrementally over a reasonable time interval. Not zero to full speed
in 1 us.
