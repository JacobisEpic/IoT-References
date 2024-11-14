# IR Beacon  -- ***Escape the Room***

You will use an IR transmit beacon based on a "TV Remote Control" that we will
provide.  Modulating the IR LED is achieved in our beacon
using the RMT function of the ESP32 to create a carrier at 38 kHz (a
standard for IR) that is and-gated by the output of the UART. The output
looks like on-off keying meshed with the carrier (see pic below).

<center><img src="../../images/ir-uart.png" width="90%" /></center>
<center> On-off keying and-gated with carrier</center>

The task at hand is to escape the room. You escape the room when you decode the message encoded in our beacon signal. To detect and decode the signal, you will need to build a few things.

In your kit, we have provided (will provide?) an IR LED and also an IR
receiver. The provided IR receiver is designed with a variable gain
amplifier and IR filter. Essentially, the IR diode will lock onto a 38
kHz carrier frequency, filter out the 38 kHz carrier, and output the
embedded pulse. This is useful in filtering out interference in the
space. The receiver is active low meaning it will output high until
data is received. Here's an example of IR modulation and received data
after the receiver.

<center><img src="../../images/ir-output receiver.png" width="80%" /></center>
<center> Receiving -- active low (Image from <a href="http://www.electronicwings.com/sensors-modules/ir-communication">ElectronicWings</a>)</center>


## Wiring

Driving the IR LED is a little bit trickier than driving a regular
LED. The IR LED requires a bit more current than what the GPIO of the
ESP32 can provide. So now what? As you may recall, we've already
encountered this problem with the DC motors. We will use one of the half-H bridge drivers on the L293D to drive the IR LED because we can use the two inputs on the half-H bridge (signal and enable)
to mix the carrier with the data.

In the exercise, we will provide the transmit beacons. But feel free to build your own if you'd like.

At the receiver, which you will build, the IR receiver just needs connections to ground, 3.3V, and the data pin to your UART input.

## Getting it to work, and finding the pesky message

The beacon is set up to modulate, via UART, a secret message. The comm
parameters that we have been using are all the same except the rate
which will be 2400 Baud to accommodate the 38kHz carrier frequency. Parity etc. will be the same as we used before.

**HINT!** The receiver is active low ... What does this mean?

## Assignment -- in class please
1. Build up an IR receiver on your ESP32
2. Program the ESP32 UART to receive 2400 Baud on the IR input channel
3. Send received bytes to the console (the USB UART channel)
4. Read the message and you can escape the room.
5. Write up results, pics, and the usual

## Reference material
- [IR Receiver Diode - TSOP38238](https://www.sparkfun.com/products/10266)
- [IR LED - 950nm](https://www.sparkfun.com/products/9349)
- [ESP RMT API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/rmt.html#)
