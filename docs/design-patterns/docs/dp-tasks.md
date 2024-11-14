# Design Pattern -- Tasks in FreeRTOS

Tasks in FreeRTOS allow independent threads of execution which can be
sheduled and prioritized by the operating system. They can be
co-dependent and exchange values with semaphores, but first things
first.

See [Tasks in FreeRTOS](https://www.freertos.org/a00015.html) as background reading.

## States
Tasks can be in the following states
- Running -- executing on one of the CPUs
- Ready -- able to run, but put on hold due to another task of higher priority
- Blocked -- waiting for some event (e.g., this is what vTaskDelay does), but the OS periodically checks them
- Suspended -- similar to Blocked, but will not be removed from this state unless explicitly called out

## Priorities

Tasks can be assigned priorities. Values range from 0 to a max defined
in FreeRTOSConfig.h. FreeRTOS has a default idle task that has the
lowest priorty which does things like garbage collection. Lower values have lower priority.

## Notes
- Tasks should not exit, or if this is desired, they should be deleted first with `vTaskDelete(Null)`
- Type `TaskFunction_t` is defined as a function that returns void and takes a void pointer as its only
parameter
- Tasks are created by `xTaskCreate()` or `xTaskCreateStatic()`, and deleted with `vTaskDelete()`



## Task Implementation

```c
	#include ...				// Includes and defines
	#define ...

	void init() {				// Convenient way to organize initialization
	     ...    				// Do it in this sub
	}

	static void task_1()			// Define your first task here
	{
		while(1){			// Or for( ;; )
			Do some stuff;		// Your task code here
		}
	}

	static void task_2()			// Define your second task here
	{
		while(1){			// Or for( ;; )
			Do some stuff;		// Your task code here
		}
	}

	voide app_main()
	{
		init();				// Initialize stuff
		xTaskCreate(task_1, "task_1",1024*2, NULL, configMAX_PRIORITIES, NULL);
		xTaskCreate(task_2, "task_2",1024*2, NULL, configMAX_PRIORITIES-1, NULL);
	}			    		// Instantiate tasks with priorites and stack size

```

## Reading
- [Example ESP32 task use for TX and RX tasks](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/uart/uart_async_rxtxtasks)
- [TaskCreate](https://www.freertos.org/a00125.html)
- [Why use an RTOS?](https://www.freertos.org/FAQWhat.html#WhyUseRTOS)
- [Multitasking](https://www.freertos.org/implementation/a00004.html)
- [Scheduling](https://www.freertos.org/implementation/a00005.html)
- [Real Time Applications](https://www.freertos.org/implementation/a00007.html)
