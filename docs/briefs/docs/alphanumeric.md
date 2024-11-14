# Setting up the Alphanumeric Display

This is a step by step guide on how to use the alphanumeric display.

<p align="center">
<img src="/docs/images/alpha.jpg" width="40%">  
</p>
<p align="center">
<i>Alphanumeric Display</i>
</p>

## Break into submodules

1. Setup ESP32 I2C
2. Set up LED Matrix
3. Bitmapping

### 1. Setup ESP32 I2C

(***Note:*** "master" and "slave" have been depreciated, but not in the
code distribution. We will use "controller" and "target" when possible.)

I2C is a two line communication protocol where one device acts as a
controller and another acts as a target. Information is piped in on a clock
cycle. The controller initiates all communication and the targets(s) know
when to listen based on hearing their address on the bus. There are some
start, stop, and acknowledgment commands built into the protocol as
well.

#### Wiring
The LED matrix has 4 simply connections: I2C (`SDA` & `SCL`), `VCC` (3.3V), and `GND`.

#### I2C Address

The default address is `0x70`. You can change the address to `0x71-0x77` as need be ([Address Jumpers](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing/pinouts#address-jumpers-2-10)).

#### Start-up routine for I2C

``` c
// Function to initiate i2c -- note the MSB declaration!
static void i2c_example_master_init() {
  // Debug
  printf("\n>> i2c Config\n");
  int err;

  // Port configuration
  int i2c_master_port = I2C_EXAMPLE_MASTER_NUM;

  // Define I2C configurations
  i2c_config_t conf;
  conf.mode = I2C_MODE_MASTER;                              // Controller mode
  conf.sda_io_num = I2C_EXAMPLE_MASTER_SDA_IO;              // Default SDA pin
  conf.sda_pullup_en = GPIO_PULLUP_ENABLE;                  // Internal pullup
  conf.scl_io_num = I2C_EXAMPLE_MASTER_SCL_IO;              // Default SCL pin
  conf.scl_pullup_en = GPIO_PULLUP_ENABLE;                  // Internal pullup
  conf.master.clk_speed = I2C_EXAMPLE_MASTER_FREQ_HZ;       // CLK frequency
  err = i2c_param_config(i2c_master_port, &conf);           // Configure
  if (err == ESP_OK) {printf("- parameters: ok\n");}

  // Install I2C driver
  err = i2c_driver_install(i2c_master_port, conf.mode,
                     I2C_EXAMPLE_MASTER_RX_BUF_DISABLE,
                     I2C_EXAMPLE_MASTER_TX_BUF_DISABLE, 0);
  if (err == ESP_OK) {printf("- initialized: yes\n\n");}

  // Data in MSB mode
  i2c_set_data_mode(i2c_master_port, I2C_DATA_MODE_MSB_FIRST, I2C_DATA_MODE_MSB_FIRST);
}
```

After setting up I2C, it is useful to send basic commands and to test
if communication works. You can build up additional utility
functions. We've included a couple in the example code.

- [Alphanumeric I2C code](https://github.com/BU-EC444/04-Code-Examples)
- [ESP-IDF I2C API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/i2c.html)
- [ESP-IDF Example code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2c)

### 2. Set up LED Matrix

The matrix driver requires some initial setup routines before it is
ready to accept commands to display alphanumerics. These are:

* Turn on the oscillator
* Set the blink rate or no blink
* Set the brightness of the display (default is off)

We pulled this information off the datasheet. Future peripherals will have different routines.

### I2C commands for the HT16K33 LED matrix
- 0x70 -- alphanumeric address
- 0x21 -- oscillator cmd
- 0x01 -- Display on cmd
- 0x00 -- Blink off cmd
- 0x80 -- Blink cmd
- 0xE0 -- Brightness cmd
This information is pulled form the datasheet.


### 3. Bitmapping
The matrix driver accepts a 16-bit binary that corresponds to some
alphanumeric. You'd want to write something that maps these
alphanumerics to their binary representation. The bitmap to 16-bit digit as follows:

<p align="center">
<img src="/docs/images/led-segment.png" width="15%"> 
</p> 
<p align="center">
<i>Segments: Image from Adafruit</i>
</p>

```
0 DP N M L K J H G2 G1 F E D C B A
```

Adafruit has a good guide:
- [Bitmap Guide](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing/usage#library-reference-4-14)
- [Bitmap Cheat](https://github.com/adafruit/Adafruit_LED_Backpack/blob/master/Adafruit_LEDBackpack.cpp)

### Example Bitmaps -- 16 bits
- 0b0101001000000001 --  T.
- 0b0101001000001111 --  D.
- 0b0100000000111001 -- C.
- 0b0100000000111000 -- L.

<center><img src="/docs/images/tdcl-display.jpg" width="70%" /></center>  
<center> </center>

### Compile and Flash

Compile and flash the example, [Alphanumeric I2C code](https://github.com/BU-EC444/04-Code-Examples), to get started.


## Reference material
- [I2C Design Pattern](https://github.com/BU-EC444/01-EBook/blob/main/docs/briefs/design-patterns/dp-i2c.md)
- [Bitmap Guide](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing/usage#library-reference-4-14)
- [Bitmap Cheat](https://github.com/adafruit/Adafruit_LED_Backpack/blob/master/Adafruit_LEDBackpack.cpp)
- [Adafruit 14-Segment Alphanumeric LED](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing)
- [Matrix Driver](https://cdn-shop.adafruit.com/datasheets/ht16K33v110.pdf)
- [Adafruit Guide](https://learn.adafruit.com/14-segment-alpha-numeric-led-featherwing?view=all)
- [Sparkfun I2C](https://learn.sparkfun.com/tutorials/i2c)
- [ESP-IDF I2C API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/i2c.html)
- [ESP-IDF Example code](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/i2c)
- [ASCII Tables](https://en.wikipedia.org/wiki/ASCII)
