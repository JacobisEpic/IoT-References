# Implement CRC on the Micro

CRC -- Cyclic Redundancy Check -- is a tool to detect errors in a
block of data. In wireless systems in which there can be packet
collisions, it is important to be able to validate the integrity of
data, and CRC (and other) methods are used for this purpose.  It's
also a good exercise in embedded coding.

In this challenge, you and your team will develop CRC functions to
generate and evaluate CRC values associated with an input string. In
the first case, you will take an input file from your local host (from
the console), generate a CRC value, and store the data in the ESP32
flash. Subsequently, you will take a second string of the same length
that is "corrupted" and generate a second CRC. Comparing the two
should produce a flag indicating the loss of integrity of the string.


## Assignment
1. Investigate techniques for creating CRCs and select an algorithm for CRC(8).
2. Select your design approach.
3. Implement your algorithm. Use of preexisting solutions is fine.
4. Agree and specify your target performance as assessment criteria
5. Test your CRC on a byte-string comprised of and ASCII representation of the Gettysburg Address. Show results.
6. Introduce an error into the test file and demonstrate detection of the error by your CRC function.
7. Write up a description of how you implemented your solution. Include
concepts, modules, APIs, tools, etc.
5. Submit a < 90s video of your report. Everyone must be on the video.

## Reference material
- [CRC Wiki](https://en.wikipedia.org/wiki/Cyclic_redundancy_check)
- [Gettysburg Address Wiki](https://en.wikipedia.org/wiki/Gettysburg_Address)
- [Gettysburg Address ASCII Test File Original](./gettysburg-original.txt)
- [Gettysburg Address ASCII Test File Changed](./gettysburg-changed.txt)
