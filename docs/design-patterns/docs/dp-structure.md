# Design Pattern -- Structuring Embedded System Programs

Design strategy:
- Event driven (external inputs or timer)
- Typically cyclic
- Main program initializes your hardware, instantiates your tasks, starts your timer
- Individual tasks run asynchronously and can communicate via queues or global variables
- Individual tasks are idle until signaled
- ISR for events (GPIO or Timer) signals to tasks


## Example 1 -- timer event driven program pattern

```c
#include stuff and defines

// Create a simple structure to pass "events" to main task

// Initialize queue handler for timer-based events

// Set up the ISR handler
{   // Prepare basic event data, aka set flag
    // Clear the interrupt
    // After the alarm triggers, we need to re-enable it to trigger it next time
    // Send the event data back to the main program task
}

// Initialize timer alarm interval and auto reload
{   // Select and initialize basic parameters of the timer 
    // Configure the alarm value and the interrupt on alarm
    // Start timer
}

// Define a single task 
static void timer_evt_task(void *arg) {
    while (1) {
        // Create dummy structure to store structure from queue
        // Transfer from queue
        // Do something here
        if (evt.flag == 1) {
            // And do something here
        }
    }
}

// Main program
void app_main(void) {
    // Create a FIFO queue for timer-event
    // Instantiate task to handle timer-based events
    // Initiate alarm for timer
}

```
