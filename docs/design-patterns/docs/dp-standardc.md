# Standard C

Standard C is a high-level programming language with low-level access
to resources like memory. Typically, code is written in C (similar to
C++) and then compiled by a compiler to run on a device (whether that
device is a microcontroller or full-fledge computer). This compiled
program known as the binary or firmware is flashed onto a
microcontroller. Finally, the binary is executed. There is a typically
a bootloader on a microcontroller that facilities initial boot
settings, flashing (saving the firmware) onto the device, and running
your program. In our class, we will:

1. Code the program
2. Compile the program
3. Flash the program
4. Execute the program
5. Monitor the program (via serial)

Here are some tutorials to get you started with C on your
computer. Note that in these tutorials the web interface is compiling
"behind the scenes" the program. You can use a compiler on your
computer such as `gcc` or `cc` on your command line. In our class, we
will setup a toolchain to compile specifically for the ESP32.

- [C Tutorials](https://www.learn-c.org)

Do a couple of the tutorials. Some more complex topics include
pointers and different type arrays.

## References:

- [Cprogramming.com](https://www.cprogramming.com/tutorial/c-tutorial.html?inl=hp)
- [Tutorials Point](https://www.tutorialspoint.com/cprogramming/index.htm)
