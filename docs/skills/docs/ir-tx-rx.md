# IR TX/RX (Updated 2023-04-14)

When one thinks wireless communication, the first thought is often
radio frequency (RF) technology: cellular (LTE), satellite (GPS),
FM/AM radio, Bluetooth, WiFi, etc. Infrared (IR) technology is an
alternate technology to RF for wireless communications and has been
around for awhile. TV remotes and Gameboy Colors (!!) are some of the
devices of yesteryear to use IR communication. Recently, IR
communication has seen a resurgence due to its line-of-sight nature
and ability to get around some of the congestion in the RF domain. 

## Protocol -- Using UART

In your kit, we have provided an IR diode and IR
receiver (TSOP diode). The provided IR receiver is designed with a
variable gain amplifier and IR filter. Essentially, the IR receiver
will lock onto a 38 kHz carrier frequency, filter out the 38 kHz
carrier, and output the embedded pulse. This is useful in filtering
out interference in the space. The TSOP diode is active low meaning it
will output high until data is received. Here's an example of IR
modulation and received data after the receiver:

<p align="center">
<img src="/docs/images/ir-output receiver.png" width="60%">
</p>
<p align="center">
<i> Image from <a href="http://www.electronicwings.com/sensors-modules/ir-communication">ElectronicWings</a></i>
</p>

For the emitter, you will need to create a 38kHz signal using the MCPWM (motor control pulse width modulation)
driver. (Note: we use this driver only for creating a 38kHz
signal.) You will also set up serial UART communications. Finally, you
can combine the two signal with on/off keying modulation with the
H-bridge.

<p align="center">
<img src="/docs/images/ir-uart.png" width="80%">
</p>
<p align="center">
<i> 38 kHz from ESP PWM and ESP UART combined and level shifted by H-bridge</i>
</p>

## Wiring
Driving the IR LED is a little bit trickier than driving a regular
LED. The IR LED requires a bit more current than what the GPIO of the
ESP32 can provide. We also want to add additional modulation to the IR
signal. The H-Bridge driver can be used here. Make sure you have the
SI part (not the TI part) which works with 3.3V logic input. Here we
can use either 3.3V or 5V on the output side. You will still need the
resistor in series. ***The Fritzing and schematic show the +Vmotor as
3.3V but this can be replaced by the USB 5V to improve the IR signal strength and thus operating
range.***

<p align="center">
<img src="/docs/images/ir-election-schem.png" width="70%">
</p>
<p align="center">
<i>IR Transmitter Module -- Schematic</i>
</p>

<p align="center">
<img src="/docs/images/ir-election_bb.png" width="80%">
</p>
<p align="center">
<i>IR Transmitter Module -- Breadboard</i>
</p>

<p align="center">
<img src="/docs/images/leader-led.png" width="50%">
</p>
<p align="center">
<i>IR Transmitter Module -- Breadboard</i>
</p>

<p align="center">
<img src="/docs/images/ir-beacon.jpg" width="60%">
</p>
<p align="center">
<i>Photo of IR Transmitter Build -- note the direction of the IR/IR Transceiver</i>
</p>


## Assignment
1. Build up ***two identical units*** of an IR emitter and IR receiver
2. To simplify this skill we are providing example code for transmitting and receiving a payload -- please see the code example provided on github
   - Uses the H-bridge to modulate UART with a 38 kHz carrier with the ESP MCPWM module
   - Modulates 'traffic light' signals in the example code (R, G, Y)
   - ***Note***: the sending and receiving do not work simultaneously in the code example. ***Only create one task or the other.***
3. Modify the code so that a button click will cause one unit to send a
code (containing the LED state -- off, red, green, yellow) to the
receiving unit. If received by the second unit, it will set its state to
the new state (off, red, green, yellow) and then light up the
appropriate LED color.
4. You can use multiple buttons as necessary
5. Write up results, pics, and the usual

## FAQ
1. ***How do I know if the IR TX and/or RX are working?***
     - ***Answer:*** You can replace the IR LED with a conventional LED and see it flickering. This is an indication that the signal is reaching the device. 
     - Use an oscilloscope to see the signal at various
points on the TX or RX signal chain. 
     - Alternatively you can set up the ESP UART to send a repeating pattern (e.g., TTTTTT...) and then
     have incoming data sent to the console

2. How do I see what is being sent as a payload?
     - Use `idf.py monitor`

## Sample IR Code
There is sample code in the code-examples folder on github. Notes:
- The configuration of your board will not exactly match the sample code (different LEDs and number)
- You will need to modify the code for your needs
- The code is designed to drive three LEDs to behave a like a traffic light. Blinking red, green, yellow lights
in sequence. Repetitively every 10s 
- For each color, the UART sends out a message via the IR output
- The receiver (on different board) is able to decode the message


## Reference material
- [IR Comms Design Pattern](/docs/design-patterns/docs/dp-irtxrx.md)
- [IR Receiver Diode - TSOP38238](https://www.sparkfun.com/products/10266)
- [IR LED - 950nm](https://www.sparkfun.com/products/9349)
- [BU EC444 code example](https://github.com/BU-EC444/04-Code-Examples/tree/main/ir-txrx-example)
