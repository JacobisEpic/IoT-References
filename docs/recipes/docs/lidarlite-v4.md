# LIDAR-lite V4 Readdressing

See reprogramming sequence in the Lidar Lite V.4 Guide

If you desire to use more than one device on the I2C bus, the devices
will need different addresses. This recipe overviews the process to
change one Lidar Lite V.4 (Garmin) Lidar addresses. For two units,
only one address needs to be changed.

For the V.4 Lidar, you will change the I2C address in flash memory of
the device. This address will persist through power cycling. 

## Steps

### Isolating the LIDARS

The first task is to isolate the LIDAR for chaning the address. Only
turn one one at a time to change the address.

### Initialize Leader

A leader device must be initialized before communicating with follower
devices.

## Change Addresses

Once the leader has been initialized the (follower) addresses of each
extra LIDAR can be changed. Changing the address on the V4 unit is
persistent -- will stay in flash memory through power cycling.

The sequence to change an address is:
1. Enable flash storage
   - Write (0xEA, 0x11)
   - Wait 100
2. Read 4-byte serial number
   - Read (0x16), data
   - Add new address to data[4]
3. Write back 5 bytes
   - Write(0x16, data)
   - Wait 100
4. Disable original addres
   - Write (0x1b, 0x01)
5. Disable flash storage
   - Write (0xEA, 0x00)
   - Wait 100


