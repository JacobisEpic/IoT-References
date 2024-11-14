# Design Pattern -- Mutual Exclusion in FreeRTOS

We have mutual exclusion to prevent deadlocks and to ensure
predictable order of execution. Why? Both of the aforementioned are
bad news for program behavior. Check it out in the reading.



See [Tasks in FreeRTOS](https://www.freertos.org/a00015.html) as background reading. 



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
- [Queues, Mutexes, Semaphores...](https://www.freertos.org/Embedded-RTOS-Queues.html)
- [Deadlock](https://en.wikipedia.org/wiki/Deadlock)
= [Readers-Writer Lock](https://en.wikipedia.org/wiki/Readers–writer_lock)
- [Mutual Exclusion](https://en.wikipedia.org/wiki/Mutual_exclusion)
- [Race Conditions(https://en.wikipedia.org/wiki/Race_condition)
