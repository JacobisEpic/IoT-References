# IR TX/RX

When one thinks wireless communication, the first thought is often
radio frequency (RF) technology: cellular (LTE), satellite (GPS),
FM/AM radio, Bluetooth, WiFi, etc. Infrared (IR) technology is an
alternate technology to RF for wireless communications and has been
around for awhile. TV remotes and Gameboy Colors (!!) are some of the
devices of yesteryear to use IR communication. Recently, IR
communication has seen a resurgence due to its line-of-sight nature
and congestion in the RF domain. One newer application of IR is in
vehicular communications, i.e. car to car communication.

In your kit, we have provided (will provide?) an IR LED and also an IR
diode. The provided IR diode is designed with a variable gain
amplifier and IR filter. Essentially, the IR diode will lock onto a 38
kHz carrier frequency, filter out the 38 kHz carrier, and output the
embedded pulse. This is useful in filtering out interference in the
space. The TSOP diode is active low meaning it will output high until
data is received. Here's an example of IR modulation and received data
after the receiver:

<center><img src="/docs/images/ir-output receiver.png" width="80%" /></center>
<center> Image from <a href="http://www.electronicwings.com/sensors-modules/ir-communication">ElectronicWings</a></center>

## Wiring

Driving the IR LED is a little bit trickier than driving a regular
LED. The IR LED requires a bit more current than what the GPIO of the
ESP32 can provide. Options are: use the H-Bridge drive part (L293D) or
a MOSFET. Here's an N-channel MOSFET switching circuit:

<center><img src="/docs/images/ir-esp32_schem.png" width="80%" /></center>
<center> MOSFET switching circuit</center>

The H-Bridge driver can be used as well. Make sure you have the LSI
part (not the TI part) which works with 3.3V logic input. Here we can
use either 3.3V or 5V on the output side. You will still need the
resistor in series.

## Protocol

There are many modulation protocols for IR and there is no real
standardization. Although, many remote manufacturers have adopted
either the SONY or NEC protocols. We're going to strip things and use
our own barebones protocol.

The ESP32 will be looking for (after the IR decoder):

- 10,000us low signal
- followed by 10,000us period comprised of:
  - high pulse corresponding to an ID (Ex: 4,000us = ID 4 and 5,000us = ID 5)
  - low pulse  completes the 10,000us period

Example signals:

<center><img src="/docs/images/4000us.png" width="100%" /></center>
<center> Transmitted and received signal for 4000us pulse</center>

<center><img src="/docs/images/5000us.png" width="100%" /></center>
<center> Transmitted and received signal for 5000us pulse</center>

## Assignment
1. Build up an IR emitter and IR receiver
2. Program the ESP32 RMT module at the emitter using a 38 kHz carrier frequency
  - Use the oscilloscope to show:
      + signal with carrier frequency
      + signal after the decoder
3. Adopt our lightweight protocol
4. Demonstrate sending different pulses, i.e., different pulse codes to light up different LEDs.
5. Write up results, pics, and the usual

## Reference material
- [IR Comms Design Pattern](/docs/briefs/docs/design-patterns/dp-irtxrx)
- [IR Receiver Diode - TSOP38238](https://www.sparkfun.com/products/10266)
- [IR LED - 950nm](https://www.sparkfun.com/products/9349)
- [ESP RMT API](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/peripherals/rmt.html#)
