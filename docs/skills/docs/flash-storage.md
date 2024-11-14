# Logging Data on the Micro -- Persistent Storage

One of the functions for many connected devices is to measure some
local sensor value and to either save it in local memory to send it
somewhere else in the networks.  This exercise focuses on the saving
locally part. And to persistent storage.


The some micros have a specialized non-volatile memory (NVM), but this
is best for small items such as device IDs and the like. There is not
usually much storage of this type.

On the ESP32, the NVM occupies space on the program (Flash) memory, so
there is actually quite a bit available if we want to use it.  We just
need to make sure that the writing step does not overrun the program
memory, and make sure that the writing process (slow) is not
interrupted by other tasks.  Fortunately, the SPI interfaces deal with
these issues.

### Notes
- The partion map shows you what part of the flash memory is being used
- You can create new partitions if you want
- Or you can use the available NVM partition for your excecise
- The NVM part has its own API which you can use

## Assignment/Specification

1. Write a program that will take text input from the console and write this to the ESP32 flash memory (or NVM)
   	 - Assume fixed length 10-character strings
   	 - Store in sequential locations associated with indices of 0-7
2. Include a way to query the device to output the string entered at a specified index.
3. Demo, report, writeup

## Reference material
- [ESP API Reference](https://esp-idf.readthedocs.io/en/latest/api-reference/storage/index.html)
