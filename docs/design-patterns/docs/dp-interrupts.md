# Design Pattern -- Interrupts

We can use interrupts to avoid the waiting associated with
polling. This idea is used to derive power savings or to avoid
blocking functions in program design.  The basic pattern is shown
below.


## Interrupt pattern for GPIO button push toggles LED (Tasks)
This code will compile with ESP distro as of 2023-09-21.

```c
/* Button Interrupt Example -- Uses Tasks */
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"
#include "esp_log.h"
#include "sdkconfig.h"

// Hardware interrupt definitions
#define GPIO_INPUT_IO_1       4
#define ESP_INTR_FLAG_DEFAULT 0
#define GPIO_INPUT_PIN_SEL    1ULL<<GPIO_INPUT_IO_1 // casting GPIO input to bitmap

int flag = 0;     // Global flag for signaling from ISR

// Define button interrupt handler -- just sets the flag on interrupt
static void IRAM_ATTR gpio_isr_handler(void* arg){
  flag = 1;
}

// Intialize the GPIO to detect button press as interrupt
static void button_init() {
  gpio_config_t io_conf;
    io_conf.intr_type = GPIO_INTR_POSEDGE; // interrupt of rising edge
    io_conf.pin_bit_mask = GPIO_INPUT_PIN_SEL; // bit mask of the pins, use GPIO4 here
    io_conf.mode = GPIO_MODE_INPUT;            // set as input mode
    io_conf.pull_up_en = 1;                    // enable resistor pull-up mode on pin
  gpio_config(&io_conf);                       // apply parameters
  gpio_intr_enable(GPIO_INPUT_IO_1 );          // enable interrupts on pin
  gpio_install_isr_service(ESP_INTR_FLAG_LEVEL3);   //install gpio isr service
  gpio_isr_handler_add(GPIO_INPUT_IO_1, gpio_isr_handler, (void*) GPIO_INPUT_IO_1); //hook isr handler for specific gpio pin
}

// Define button task that runs forever
void button_task(){
  while(1) {                               // loop forever in this task
    if(flag) {
      printf("Button pressed.\n");
      flag = 0;                            // set the flag to false
    }
    vTaskDelay(100 / portTICK_PERIOD_MS);  // wait a bit
  }
}

// The main program (1) intializes the button interrupts and (2) starts the task
void app_main(void)  // 
{
  button_init();     // Initialize button config 
  xTaskCreate(button_task, "button_task", 1024*2, NULL, configMAX_PRIORITIES, NULL); // Create task
  printf("Everything initialized. Waiting for button presses...\n"); // console message that it has begun
  while(1) {                               // loop forever in this task
    vTaskDelay(100 / portTICK_PERIOD_MS);  // wait a bit
  }

}

```
## Interrupt pattern for GPIO button push toggles LED (no Tasks)
This code will compile with ESP distro as of 2023-09-21.

```c

/* Button Interrupt Example -- No Tasks*/
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"
#include "esp_log.h"
#include "sdkconfig.h"

// Hardware interrupt definitions
#define GPIO_INPUT_IO_1       4
#define ESP_INTR_FLAG_DEFAULT 0
#define GPIO_INPUT_PIN_SEL    1ULL<<GPIO_INPUT_IO_1 // casting GPIO input to bitmap

int flag = 0;     // Global flag for signaling from ISR

// Define button interrupt handler -- just sets the flag on interrupt
static void IRAM_ATTR gpio_isr_handler(void* arg){
  flag = 1;
}

// Intialize the GPIO to detect button press as interrupt
static void button_init() {
  gpio_config_t io_conf;
    io_conf.intr_type = GPIO_INTR_POSEDGE;     // interrupt of rising edge
    io_conf.pin_bit_mask = GPIO_INPUT_PIN_SEL; // bit mask of the pins, use GPIO4 here
    io_conf.mode = GPIO_MODE_INPUT;            // set as input mode
    io_conf.pull_up_en = 1;                    // enable resistor pull-up mode on pin
  gpio_config(&io_conf);                       // apply parameters
  gpio_intr_enable(GPIO_INPUT_IO_1 );          // enable interrupts on pin
  gpio_install_isr_service(ESP_INTR_FLAG_LEVEL3);   //install gpio isr service
  gpio_isr_handler_add(GPIO_INPUT_IO_1, gpio_isr_handler, (void*) GPIO_INPUT_IO_1); //hook isr handler for specific gpio pin
}


// The main program (1) intializes the button interrupts and (2) loops
 void app_main(void)   
{
  button_init();     // Initialize button config 
  printf("Everything initialized. Waiting for button presses...\n"); // console message that it has begun

  while(1) {                               // loop forever in this task
    if(flag) {
      printf("Button pressed.\n");
      flag = 0;                            // set the flag to false
    }
    vTaskDelay(100 / portTICK_PERIOD_MS);  // wait a bit
  }
}

```

In these examples, the ISR only changes a flag. But the ISR removes any
blocking due to polling.

## Additional Resources
- [ESP IDF Example for GPIO Interrupt](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/gpio/generic_gpio)
- [EC444 Code Example](https://github.com/BU-EC444/04-Code-Examples/tree/main/button-timer)