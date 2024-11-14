# LIDAR-lite V3 Readdressing

### Author: Daniel Paganelli

3/24/2023

The LIDAR-lite V3 device boots with a default I2C address. If you wish
to use two or more devices on the same bus, then you will need to
change the adress of the additional units to avoid the addressing
conflict.  This document describes how to switch-out the addresses.

## Steps

### Isolating the LIDARS

The first task is to isolate each LIDAR on the I2C bus. This means
disabling (but not turning off) all but one device while resetting the
address. The default 'follower' address is 0x62. 'Disabling' is done
by driving the orange enable wire to logic zero using a GPIO pin (you
will need to do this for each extra LIDAR on the bus). That is, at the start of
the address changing process, disable all but a single LIDAR.

### Initialize Leader

A leader device must be initialized before communicating with follower
devices. That can be done with the following function:
```
static void i2c_master_init(){
  printf("\n>> i2c Config\n");  // For debugging
  int err;

  // Port configuration
  int i2c_master_port = I2C_EXAMPLE_MASTER_NUM;

  // Define I2C configurations
  i2c_config_t conf;
  conf.mode = I2C_MODE_MASTER;                              // Master mode
  conf.sda_io_num = I2C_EXAMPLE_MASTER_SDA_IO;              // Default SDA pin
  conf.sda_pullup_en = GPIO_PULLUP_ENABLE;                  // Internal pullup
  conf.scl_io_num = I2C_EXAMPLE_MASTER_SCL_IO;              // Default SCL pin
  conf.scl_pullup_en = GPIO_PULLUP_ENABLE;                  // Internal pullup
  conf.master.clk_speed = I2C_EXAMPLE_MASTER_FREQ_HZ;       // CLK frequency
  conf.clk_flags = 0;
  err = i2c_param_config(i2c_master_port, &conf);           // Configure
  if (err == ESP_OK) {printf("- parameters: ok\n");}

  // Install I2C driver
  err = i2c_driver_install(i2c_master_port, conf.mode,
                     I2C_EXAMPLE_MASTER_RX_BUF_DISABLE,
                     I2C_EXAMPLE_MASTER_TX_BUF_DISABLE, 0);
  if (err == ESP_OK) {printf("- initialized: yes\n");}

  // Data in MSB mode
  i2c_set_data_mode(i2c_master_port, I2C_DATA_MODE_MSB_FIRST, I2C_DATA_MODE_MSB_FIRST);
}
```

## Change Addresses

Once the leader has been initialized the (follower) addresses of each extra LIDAR can
be changed. This function does so cleanly. For a better understanding
of what it actually does, see the [V3 LIDARlite
manual](https://support.garmin.com/en-US/?partNumber=010-01722-00&tab=manuals).


```
static void change_addr(){
    
    uint16_t serial = readRegister(0x96, LIDARLite_ADDRESS);
    printf("Serial Number: %x\n", serial);
    
    int high    = (serial>>8) & 0xff;
    int low     = serial & (0xff);

    writeRegister(0x18, high, LIDARLite_ADDRESS);
    writeRegister(0x19, low, LIDARLite_ADDRESS);

    writeRegister(0x1a, 0x50, LIDARLite_ADDRESS);
    writeRegister(0x1e, 0x08, LIDARLite_ADDRESS);
    printf("Changed Address!");
}
```

The following `readRegiste()r` and `writeRegister()` support the function above. 


Function to read one byte from a register
```
// Function to read register (single byte read)
uint16_t readRegister(uint8_t reg, int addr) {

uint8_t data1; //first byte MSB
  uint8_t data2; //second byte LSB

  i2c_cmd_handle_t cmd = i2c_cmd_link_create();
  i2c_cmd_handle_t cmd1 = i2c_cmd_link_create();

  // Start
  i2c_master_start(cmd);
  // Master write follower address + write bit
  i2c_master_write_byte(cmd, ( addr << 1 ) | WRITE_BIT, I2C_MASTER_ACK); 
  // Master write register address + send ack
  i2c_master_write_byte(cmd, reg, I2C_MASTER_ACK); 
  // master stops
  i2c_master_stop(cmd);
  // This starts the I2C communication
  i2c_master_cmd_begin(I2C_EXAMPLE_MASTER_NUM, cmd, 1000 / portTICK_PERIOD_MS); 
  i2c_cmd_link_delete(cmd);

  // master starts
  i2c_master_start(cmd1);
  // Master write follower address + read bit
  i2c_master_write_byte(cmd1, ( addr << 1 ) | READ_BIT, I2C_MASTER_ACK);  
  // Master reads in follower ack and data
  i2c_master_read_byte(cmd1, &data1 , I2C_MASTER_ACK);
  i2c_master_read_byte(cmd1, &data2 , I2C_MASTER_NACK);
  // Master nacks and stops
  i2c_master_stop(cmd1);
  // This starts the I2C communication
  i2c_master_cmd_begin(I2C_EXAMPLE_MASTER_NUM, cmd1, 1000 / portTICK_PERIOD_MS); 
  i2c_cmd_link_delete(cmd1);
  

  uint16_t two_byte_data = (data1 << 8 | data2);
  return two_byte_data;
}
```
Function to write one byte to register
```
// Function to write one byte to register (single byte write)
void writeRegister(uint8_t reg, uint8_t data, int addr) {

// create i2c communication init
  i2c_cmd_handle_t cmd = i2c_cmd_link_create();
  i2c_master_start(cmd);	// 1. Start (Master write start)
  i2c_master_write_byte(cmd, ( addr << 1 ) | WRITE_BIT, I2C_MASTER_ACK); // (Master write follower add + write bit)
  // wait for salve to ack
  i2c_master_write_byte(cmd, reg, I2C_MASTER_ACK); // (Master write register address)
  // wait for follower to ack
  i2c_master_write_byte(cmd, data, I2C_MASTER_ACK);// master write data 
  // wait for follower to ack
  i2c_master_stop(cmd); // 11. Stop
  // i2c communication done and delete
  i2c_master_cmd_begin(I2C_EXAMPLE_MASTER_NUM, cmd, 1000 / portTICK_PERIOD_MS);
  i2c_cmd_link_delete(cmd);
  // no return here since data is written by master onto follower
}
```

Once the address of one LIDAR has been changed you can run a simple
function (i2c_scanner and its support, testConnection) to confirm the
LIDAR's address has changed. If it has, turn the next LIDAR on by
setting its enable pin to high and repeat the process.

```
// Utility function to test for I2C device address -- not used in deploy
int testConnection(uint8_t devAddr, int32_t timeout) {
  i2c_cmd_handle_t cmd = i2c_cmd_link_create();
  i2c_master_start(cmd);
  i2c_master_write_byte(cmd, (devAddr << 1) | I2C_MASTER_WRITE, ACK_CHECK_EN);
  i2c_master_stop(cmd);
  int err = i2c_master_cmd_begin(I2C_EXAMPLE_MASTER_NUM, cmd, 1000 / portTICK_PERIOD_MS);
  i2c_cmd_link_delete(cmd);
  return err;
}
// Utility function to scan for i2c device
static void i2c_scanner() {
  int32_t scanTimeout = 1000;
  printf("\n>> I2C scanning ..."  "\n");
  uint8_t count = 0;
  for (uint8_t i = 1; i < 127; i++) {
    if (testConnection(i, scanTimeout) == ESP_OK) {
      printf( "- Device found at address: 0x%X%s", i, "\n");
      count++;
    }
  }
  if (count == 0) {printf("- No I2C devices found!" "\n");}
}
// i2c init from Master init
```

### Common issues

The wires on the LIDARS are very fragile. If they get knocked out, the
program will run through the entire address change process without an
error.  The way to determine this has occured is if the task that is
sampling the LIDAR after the address has been set blocks when it tries
to sample.






