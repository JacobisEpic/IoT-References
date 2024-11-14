# Console I/O

In standard C, the console I/O is to `stdout` and from `stdin`,
usually the display and keyboard attached to a terminal program of
your laptop.

Then the usual functions to write and read are:

```c
	printf();		// print formatted data to stdout
	scanf();		// read formatted data from stdin
	putchar();		// print single char to stdout
	getchar();		// read single char from stdin
	puts();			// print string to stdout
	gets();			// read string from stdin
```

But the ESP32 needs to be configured to be able to respond to your
keyboard and display.  At the 'laptop' end, you will implement a
program that creates a virtual display and keyboard that will talk to
your USB port. USB is serial; your ESP32 will talk to the serial port
with the two wire TX/RX of the ESP32 UART. 

***Note that the Echo program in the ESP32 repo refers to the UART 1.*** This needs to be changed
for the Adafruit Huzzah board: The default UART is
`UART_NUM_0` with Baud rate `115200`.`UART_NUM_0` is attached to
`GPIO1` for the TX pin and to `GPIO3` for the RX pin. ***UART for console
output is enabled by default*** and can be changed in menuconfig.

## Client Side (your laptop)

For Windows, the laptop client is a program like `putty` that
implements serial communications to a COM / USB port.  For linux or
the mac, this can be realized using `CoolTerm`. You will need to
know which device the ESP32/USB is attached to (find it in /dev/ --
the command for unix is `ls /dev/tty.*` or `ls /dev/cu.*`). (Note: each of these programs provides
a `monitor`-like console for input (keyboard) and output (console)).

For the mac, we recommend `CoolTerm` which can be installed from here: http://freeware.the-meiers.org.


## ESP32 side

Make sure that you have identified the pins and port used by the ESP32/Huzzah
for the USB connector. As per the earlier note. 

### Notes on Standard I/O

The basic pattern for configuring using standard I/O to read and write
using `printf()`, `puts()`, `getchar()`, and `putchar()` is:


```c

#include <stdio.h>

void app_main()
{
    // Here we are using stdio printf() and puts()
    int test = 123;
    printf("Hello World!\n");
    printf("Test: %d\n",test);
    puts("--------------------------");

    uint8_t ch;

    while(1) {

      // Here we are using stdio getchar() and putchar()
      ch = getchar();
      if (ch!=0xFF)
      {
         putchar(ch);    
      }

      vTaskDelay(50 / portTICK_PERIOD_MS);
    }
}
```

***BUT,*** Reading strings in from `stdin` is not reliable in the standard ESP32
configuration due to the ESP32 console's default non-blocking read
behavior. This means the ESP32 returns data present in `stdin`
continuously. As such, you won't be able to enter more than one
character. Functions `scanf()` and `gets()` will not work reliably for
this reason. This can be remedied by using the UART driver, which
enables blocking on read and write. (Write is configured in the ESP32
console to be blocking by default.)

### Using the UART driver

By using the UART driver described [here, for
VFS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/storage/vfs.html?highlight=esp_vfs_dev#standard-io-streams-stdin-stdout-stderr),
you will be using a version that permits blocking for regular stdio
functions.

Thus, you can enter full strings and numbers with more than one
digit. This design pattern is shown below: (this example will compile and can be found in the course examples repo).

```c
/* From design pattern Serial IO Example */
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"
#include "esp_log.h"
#include "sdkconfig.h"

#include <stdio.h>
#include <string.h>
#include "driver/uart.h"
#include "esp_vfs_dev.h"
// This is associated with VFS -- virtual file system interface and abstraction -- see the docs

void app_main()
{
    /* Install UART driver for interrupt-driven reads and writes */
    ESP_ERROR_CHECK( uart_driver_install(UART_NUM_0,
      256, 0, 0, NULL, 0) );

    /* Tell VFS to use UART driver */
    esp_vfs_dev_uart_use_driver(UART_NUM_0);

    int num = 0;

    while(1) {
      // gets()
      char buf[5];
      gets(buf);
      if (buf[0] != '\0') {
       printf("string is: %s\n", buf);
      }

      // scanf()
      printf("Enter a number: \n");
      scanf("%d", &num);
      printf("Got: %d\n", num);

      vTaskDelay(50 / portTICK_PERIOD_MS);
    }
}
```

This following is a second approach: take control of the UART behavior
directly. You can bypass `stdio` and read from and write to the UART
port directly. The basic pattern for configuring the UART and reading
and writing directly from UART is: (this example needs you to identify some of the
UART settings before it will compile)

```c
#include "driver/uart.h		// Include UART header

#define XYZ			// Define your UART pins

void app_main() {		// Your main program
	.baud_rate =   		// Assign values to UART data structure
	.data_bits =
	.parity =
	.stop_bits =
	.flow_control =

	uart_			// Write above values to config UART
	uart_set_pin		// Configure pins
	uart_driver_install	// Install UART driver

	uint8_t *data = 		// Instantiate UART buffer

	while (1) {			// Loop indefinitely reading or writing

		uart_read_bytes()	// Read data from UART
		uart_write_bytes()	// Or write to UART
	}
}
```

This is also documented in the ESP32 echo example and the
ESP32 IDF Programming guide.

## References

- [ESP32 Echo Example from Course Repo](https://github.com/BU-EC444/04-Code-Examples/tree/main/echo)
- [ESP-IDF Programming Guide: UART](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/uart.html)
- [Standard I/O Stream](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/storage/vfs.html#standard-io-streams-stdin-stdout-stderr)
- [VFS to change behiavior of stdio input](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/storage/vfs.html?highlight=esp_vfs_dev#standard-io-streams-stdin-stdout-stderr)

