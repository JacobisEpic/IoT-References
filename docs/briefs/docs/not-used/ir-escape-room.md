# IR Beacon --  ***Escape the Room***

## [Background for this Skill](/docs/briefs/design-patterns/dp-irtxrx)

You will use an IR transmit beacon based on a "TV Remote Control" that
we will provide.  Modulating the IR LED is achieved in our beacon
using the RMT function of the ESP32 to create a carrier at 38 kHz (a
standard for IR) that is and-gated by the output of the UART. The
output looks like on-off keying meshed with the carrier (see pic
below).

<p align="center">
<img src="/images/ir-uart.png" width="90%">
</p>
<p align="center">
<i> On-off keying and-gated with carrier</i>
</p>

***The first step is to decode the message embedded in each of the beacon signals.***

***Then the codes are used to find the next clue.***

***You escape the room when the combination lock is opened.***

To detect and decode the signal, you will need to build a few things.
In your kit, we will provide an IR LED and also an IR
receiver. The provided IR receiver is designed with a variable gain
amplifier and IR filter. Essentially, the IR diode will lock onto a 38
kHz carrier frequency, filter out the 38 kHz carrier, and output the
embedded pulse. This is useful in filtering out interference in the
space. The receiver is active low meaning it will output high until
data is received.

<!-- Here's an example of IR modulation and received data after the receiver. -->


<!--

## Wiring

The IR LED requires more drive current which means that we need
additional electronics in order to drive it -- a GPIO pin will be challenged to
source sufficient current. But recall that this is the same problem
for the DC motor control. Enter the H-bridge again.

The H-bridge has an added feature that we can "mix" a bit stream with
a binary modulation which is exactly what the TV remote control
does. Later, we can modulate other high current devices, including a
laser.

For the exercise, ***we will provide the beacons***, but you may want to
create your own beacons later.

-->

<!--

### Beacon Wiring


You do not need to build the transmit module for this skill, but we
are providing the schematic for future use.

<center><img src="/images/ir-escape_schem.png" width="70%" /></center>
<center>IR Transmitter Module -- Schematic</center>

<center><img src="/images/ir-escape_bb.png" width="80%" /></center>
<center>IR Transmitter Module -- Breadboard</center>

-->

### Receiver Wiring


At the receiver, the IR receiver just needs ground, 3.3V, and connect
the data pin to your UART input.

<p align="center">
<img src="/images/TSOP382.png" width="40%">
</p>
<p align="center">
<i>IR Receiver Module</i>
</p>

<p align="center">
<img src="/images/ir-rcv_bb.png" width="100%">
</p>
<p align="center">
<i>IR Receiver Wiring</i>
</p>

## Getting it to work, and finding the pesky message

The beacon is set up to modulate, via UART, a secret message. The comm
parameters that we have been using are all the same except the rate
which will be 2400 Baud to accommodate the 38kHz carrier
frequency.. Parity etc. will be the same as we used before.

**HINT!** The receiver is active low ... What does this mean?


## Assignment -- *in class please*
1. Build up an IR receiver on your ESP32
2. Program the ESP32 UART to receive 2400 Baud on the IR input channel
3. Send received bytes to the console (the USB UART channel)
4. Read the message from each beacon and figure out the clues
5. Follow the clues to the next clue...
6. Unlock the lock and escape the room
5. Post some artifacts to your team repo

## Reference material
- [IR Receiver Diode - TSOP38238](https://www.sparkfun.com/products/10266)
- [IR LED - 950nm](https://www.sparkfun.com/products/9349)
- [ESP RMT API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/rmt.html#)

_____

<p align="center">
<img src="/images/lockbox.jpg" width="80%">
</p>
<p align="center">
<i>Code Opens the Lockbox</i>
</p>
