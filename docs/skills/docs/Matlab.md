# Matlab Interfacing for Data Visualization


The ESP32 can source data via serial port (USB), via network sockets,
for by any other code that deliver to a well defined interface.
Matlab can then be used to interface to the data stream whether static
or dynamic. We have used both approaches.

For the file approach, the ESP32 data is put into a file in the most
convenient way. Then a Matlab script opens the file, tests for
updates, if any. If there are updates, data are read into Matlab
appended to existing data structures and displayed, possibly in real
time.

For the serial port or sockets approach, Matlab can open equivalent
interfaces to receive data serially, again, in real time. This
approach should be designed with error handling to ensure that
corrupted data does not hang the application.

There is not an active skill assignment here, but if you would like to
use Matlab for visualization, we can provide sample code for the file
read or serial port read.

  