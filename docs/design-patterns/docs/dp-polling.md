# Design Pattern -- Polling 

We define polling here as camping on some input (e.g., ADC, GPIO) to
see if the value changes. The problem with polling is that it usually
consumes CPU cycles while waiting for some unpredictable future
event. But polling is a simple and useful technique tha can be
optimized with more cycle-efficient approaches.

## Polling example with ADC

The basic pattern is

```c
	#include XYZ			// Your includes
	#define XYZ			// Your defines, including ADC pins

	void app_main() {		// Your main program
	     adc1_config...		// Configure ADC

	     uint32_t adc_reading =0;	// Some temp value of ADC

	     while (adc_reading < 1048) { // Loop until value > 1048

	    	  adc_reading = adc1_get_raw()	// Get ADC value

		  }
	}
```

That's it. Parked on the continuous reading of the value until it
reaches 1048.

The polling example contrasts with the pattern for interrupts.

