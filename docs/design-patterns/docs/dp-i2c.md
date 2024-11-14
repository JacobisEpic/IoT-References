# I2C

I2C stands for Inter-Integrated Circuit and allows for multiple slave
devices to connect to the same bus as long as they are differentiated
by an ID address, typically there are 112 possible addresses (7-bits
with some reserved addresses); new standards have increased to 10-bit
addresses. I2C requires only 2 pins: one for a data signal and another
for a clock signal. Unlike UART, the clock signal synchronizes devices
and devices do not need to know clock frequency ahead of time. And
compared to SPI, less pins are required (2 compared to 4 in SPI) by
sacrificing some speed and full duplex communications.

[Sparkfun](https://learn.sparkfun.com/tutorials/i2c) has a good read
on I2C if you want to read into the protocol and clocking
methodology. In this stub, we're going to focus on setting up I2C for
the ESP32 using the ADXL343 has an example sensor.

## Wiring I2C

<p align="center">
<img src="/docs/images/i2c-wiring.png" width="70%">  
</p>
<p align="center">
<i> From Analog Devices </i>
</p>

(***Note:*** "master" and "slave" have been depreciated, but not in the
code distribution. We will use "controller" and "target" when possible.)

In I2C, the controller commands the target and initiates all
communications. The two lines of I2C are typically tied high (to Vcc)
loosely with pull-up resistors (~10k). Multiple targets can connect to
the clock (SCL) and data lines (SDA). In our scenario, the ESP32 is
the controller and peripheral devices are targets.

## Configure I2C driver

This is a sample configuration of I2C following the ESP32 guide. There
are two I2C ports. Remember to define your I2C lines to pins 22 (SCL)
and 23 (SDA), which corresponds to the silkscreen on the Adafruit
Feather Huzzah. We also configure internal pull up resistors for both
lines and a clock frequency of 100kHz. Also, included in the defines
are definitions for acknowledgments and read/write bits.

``` c
// Controller I2C
#define I2C_EXAMPLE_MASTER_SCL_IO          22   // gpio number for i2c clk
#define I2C_EXAMPLE_MASTER_SDA_IO          23   // gpio number for i2c data
#define I2C_EXAMPLE_MASTER_NUM             I2C_NUM_0  // i2c port
#define I2C_EXAMPLE_MASTER_TX_BUF_DISABLE  0    // i2c controller no buffer needed
#define I2C_EXAMPLE_MASTER_RX_BUF_DISABLE  0    // i2c controller no buffer needed
#define I2C_EXAMPLE_MASTER_FREQ_HZ         100000     // i2c controller clock freq
#define WRITE_BIT                          I2C_MASTER_WRITE // i2c controller write
#define READ_BIT                           I2C_MASTER_READ  // i2c controller read
#define ACK_CHECK_EN                       true // i2c controller will check ack
#define ACK_CHECK_DIS                      false// i2c controller will not check ack
#define ACK_VAL                            0x00 // i2c ack value
#define NACK_VAL                           0xFF // i2c nack value

// ADXL343
#define SLAVE_ADDR                         ADXL343_ADDRESS // 0x53
```

``` c
// Port configuration
int i2c_master_port = I2C_EXAMPLE_MASTER_NUM;

/// Define I2C configurations
i2c_config_t conf;
conf.mode = I2C_MODE_MASTER;                              // Controller mode
conf.sda_io_num = I2C_EXAMPLE_MASTER_SDA_IO;              // Default SDA pin
conf.sda_pullup_en = GPIO_PULLUP_ENABLE;                  // Internal pullup
conf.scl_io_num = I2C_EXAMPLE_MASTER_SCL_IO;              // Default SCL pin
conf.scl_pullup_en = GPIO_PULLUP_ENABLE;                  // Internal pullup
conf.master.clk_speed = I2C_EXAMPLE_MASTER_FREQ_HZ;       // CLK frequency
err = i2c_param_config(i2c_master_port, &conf);           // Configure
if (err == ESP_OK) {printf("- parameters: ok\n");}
```

## Install Driver
Like the other peripherals, you have to install your I2C driver 
after configuring it. We take an additional step to define data in MSB mode.

``` c
// Install I2C driver
err = i2c_driver_install(i2c_master_port, conf.mode,
	 I2C_EXAMPLE_MASTER_RX_BUF_DISABLE, I2C_EXAMPLE_MASTER_TX_BUF_DISABLE, 0);
if (err == ESP_OK) {printf("- initialized: yes\n");}

// Data in MSB mode
i2c_set_data_mode(i2c_master_port, I2C_DATA_MODE_MSB_FIRST, I2C_DATA_MODE_MSB_FIRST);
```

## Controller Mode Communications

Communication with I2C requires clocking data out with precise
timing. Fortunately, the ESP32 takes care of this and we only have to
deal with formatting the command payload. We are using the ADXL343 as
an example device. There are four ways to communicate with the device
using I2C shown below: single-byte write, multiple-byte write,
single-byte read, and multiple-byte read. We work out single-byte read
(red box). You will need to work out the other commands for the
accelerometer skill.

<p align="center">
<img src="/docs/images/ADXL343-i2c.png" width="100%">  
</p>
<p align="center">
<i>From ADXL343 Datasheet</i>
</p>

The ESP32 I2C api lets you define your command to match communication
protocols specified by device datasheets. If you look at the blue box
above, you will see that the communication structure is:

1. **Controller** write `Start`
2. **Controller** write `Target address + Write bit`
3. **Controller** waits for `ACK` from *Target*
4. **Controller** write `register address`
5. **Controller** waits for `ACK` from *Target*
6. **Controller** write `Start` again
7. **Controller** write `Target address + Read bit`
8. **Controller** waits for `ACK` from *Target*
9. **Controller** waits for `Data` from *Target*
10. **Controller** writes `NACK`
11. **Controller** writes `Stop`

The below code sets up an I2C communication command that follow just
that. See if you can match the 11 steps to code below.

``` c
// Get Device ID
int getDeviceID(uint8_t *data) {
  int ret;
  i2c_cmd_handle_t cmd = i2c_cmd_link_create();
  i2c_master_start(cmd);	// 1. Start
  i2c_master_write_byte(cmd, ( SLAVE_ADDR << 1 ) | WRITE_BIT, ACK_CHECK_EN); // 2.-3.
  i2c_master_write_byte(cmd, ADXL343_REG_DEVID, ACK_CHECK_EN); // 4.-5.
  i2c_master_start(cmd); // 6.
  i2c_master_write_byte(cmd, ( SLAVE_ADDR << 1 ) | READ_BIT, ACK_CHECK_EN);  // 7.-8.
  i2c_master_read_byte(cmd, data, ACK_CHECK_DIS); // 9.-10.
  i2c_master_stop(cmd); // 11. Stop
  ret = i2c_master_cmd_begin(I2C_EXAMPLE_MASTER_NUM, cmd, 1000 / portTICK_RATE_MS); // This starts the I2C communication
  i2c_cmd_link_delete(cmd);
  return ret;
}
```

## Reference Material
- [Analog Devices I2C Primer](https://www.analog.com/en/technical-articles/i2c-primer-what-is-i2c-part-1.html)
- [Sparkfun I2C](https://learn.sparkfun.com/tutorials/i2c)
- [ADXL343 Base Code](https://github.com/BU-EC444/04-Code-Examples/tree/master/i2c-display)
- [ADXL343 Datasheet](https://cdn-learn.adafruit.com/assets/assets/000/070/556/original/adxl343.pdf?1549287964)
- [Adafruit Learn Guide on the ADXL343](https://learn.adafruit.com/adxl343-breakout-learning-guide/overview)
- [Adafruit Example Code](https://github.com/adafruit/Adafruit_ADXL343)
- [ESP-IDF I2C API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/i2c.html)
- [ESP-IDF Example code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2c)
