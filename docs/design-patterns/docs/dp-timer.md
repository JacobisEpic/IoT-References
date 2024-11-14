# Design Pattern -- Timer Interrupts

Timer interrupts are similar to GPIO interrupts except the interrupt
is tied to the timer instead. In this manner, you can set a timer to
interrupt at a set interval to implement some function.

The below code is an example to setup a repeating timer interval alarm
that triggers an interrupt.  The interrupt passes the alarm onward via
a queue to the main task. The code runs as-is and can be found on our
GitHub [code-examples
repo](https://github.com/BU-EC444/04-Code-Examples/tree/master/timer-example-new).

Note that this example introduces the important ***queue*** and
***queue handle*** concepts that allow tasks to send and receive
events.

## Timer Interrupt pattern:

```c
/* This is an example of a single timer interrupt using the ESP GPTimer APIs
   The example is pulled from 
   https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/gptimer.html#
   The timer triggers an event every 10s which is sent from the ISR/callback via an event queue
   The Event in queue signals action to turn on LED for 1s
   Runs in latest ESP32 distro as of 2023/09/22
*/

#include <stdio.h>
#include <string.h>
#include <stdlib.h>             
#include <inttypes.h>           
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "freertos/queue.h"     
#include "esp_log.h"            // for error logging
#include "esp_system.h"         
#include "driver/uart.h"
#include "driver/gptimer.h"     
#include "driver/gpio.h"        
#include "driver/ledc.h"        

#define ONBOARD   13  // onboard LED
#define GPIO_OUTPUT_PIN_SEL  (1ULL<<ONBOARD)

// Global flag
bool flag = false;

// Initialize GPIO for LED signals
static void led_init() {
    gpio_config_t io_conf = {};        // zero-initialize the config structure
    io_conf.mode = GPIO_MODE_OUTPUT;   // set as output mode
    io_conf.pin_bit_mask = GPIO_OUTPUT_PIN_SEL; // bit mask of the pins that you want to set
    io_conf.pull_down_en = 0;          // disable pull-down mode
    io_conf.pull_up_en = 0;            // disable pull-up mode
    gpio_config(&io_conf);             // configure GPIO with the given settings
}

// A simple structure for queue elements
typedef struct {
    uint64_t event_count;
} example_queue_element_t;

// Create a FIFO queue for timer-based events
example_queue_element_t ele;
QueueHandle_t timer_queue;

// System log tags -- get logged when things happen, for debugging 
static const char *TAG_TIMER = "ec444: timer";       

// Timer interrupt handler -- callback timer function -- from GPTimer guide example
static bool IRAM_ATTR timer_on_alarm_cb(gptimer_handle_t timer, const gptimer_alarm_event_data_t *edata, void *user_data) {
    BaseType_t high_task_awoken = pdFALSE;
    QueueHandle_t timer_queue1 = (QueueHandle_t)user_data;    // represents state info passed to callback, if needed
    example_queue_element_t ele = {
          .event_count = edata->count_value                   // Retrieve count value and send to queue
      };
    xQueueSendFromISR(timer_queue1, &ele, &high_task_awoken); // Puts data into queue and alerts other recipients
    return (high_task_awoken == pdTRUE);  		      // pdTRUE indicates data posted successfully
}

// Timer configuration -- from GPTimer guide example
static void alarm_init() {
    gptimer_handle_t gptimer = NULL;
    gptimer_config_t timer_config = {
      .clk_src = GPTIMER_CLK_SRC_DEFAULT,
      .direction = GPTIMER_COUNT_UP,
      .resolution_hz = 1000000, // 1MHz, 1 tick=1us
    };
    ESP_ERROR_CHECK(gptimer_new_timer(&timer_config, &gptimer)); // instantiates timer
  
    gptimer_event_callbacks_t cbs = { // Set alarm callback
      .on_alarm = timer_on_alarm_cb,  // This is a specific supported callback from callbacks list
    };
    ESP_ERROR_CHECK(gptimer_register_event_callbacks(gptimer, &cbs, timer_queue)); // This registers the callback
    ESP_ERROR_CHECK(gptimer_enable(gptimer));                                      // Enables timer interrupt ISR

    ESP_LOGI(TAG_TIMER, "Start timer, update alarm value dynamically and auto reload"); 
    gptimer_alarm_config_t alarm_config = { // Configure the alarm 
      .reload_count = 0,                    // counter will reload with 0 on alarm event
      .alarm_count = 10*1000000,            // period = 10*1s = 10s
      .flags.auto_reload_on_alarm = true,   // enable auto-reload
    };
    ESP_ERROR_CHECK(gptimer_set_alarm_action(gptimer, &alarm_config));  // this enacts the alarm config
    ESP_ERROR_CHECK(gptimer_start(gptimer));                            // this starts the timer
}

// LED task to light LED based on alarm flag
void led_task(){
  while(1) {
    if (flag) {                             // Uses flag set by Timer task; could be moved to there
        gpio_set_level(ONBOARD, 1);
	flag = !flag;
      }
    vTaskDelay(1000 / portTICK_PERIOD_MS);
    gpio_set_level(ONBOARD, 0);
  }
}


// Timer task -- what to do when the timer alarm triggers 
static void timer_evt_task(void *arg) {
  while (1) {
    // Transfer from queue and do something if triggered
    if (xQueueReceive(timer_queue, &ele, pdMS_TO_TICKS(2000))) {
      printf("Action!\n");
      flag = true;           // Set a flag to be used elsewhere 
    }
  }
}

void app_main() {
  // Timer queue initialize 
  timer_queue = xQueueCreate(10, sizeof(example_queue_element_t));
  if (!timer_queue) {
    ESP_LOGE(TAG_TIMER, "Creating queue failed");
    return;
  }

  // Create task to handle timer-based events 
  xTaskCreate(timer_evt_task, "timer_evt_task", 2048, NULL, 5, NULL);

  // Create task to use LED based on flag
  xTaskCreate(led_task, "led_task", 2048, NULL, 5, NULL);

  // Initialize all the things
  led_init();
  alarm_init();
 
}
```