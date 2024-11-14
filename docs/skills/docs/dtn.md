# DTN

What the heck is DTN and why is it in my course?

DTN stands for 'delay tolerant networking.' And it shows up in
applications where parts of the network might be unreachable or some
of the devices/nodes might be periodically unavailable.

A classic example of DTN is email. It does not need to be delivered
nor responed to immediately (although some differ on this
point). Email is delivered in a 'store-and-forward' way. If a next
destination is not available it can be held and sent when a connection
is available.

DTN is expected to play a role in interplanetary networks where
connections are intermitten at best.

In most of the ESP32 applications we have developed so far, data are
sent when they are available. But what if a connection is not
available when data are sourced? Are the data dropped?  In some cases
this is ok, such as when there is redundancy (e.g., temperature
readings). In other cases, we need to save the data and send them
later when a connection is available.

So what is the exercise here:

## Assignment
1. Let's reuse the code from thermistor-sensing.
2. Sample data every second, save, and send to your server with confirmation of reception
3. When reception is complete, you can discard the data from your ESP
4.  If the server is not available, you need to save the data until it can be sent later
5. When the server becomes available, transfer the data, receiving acknowledgements, and remove accumulated data from your ESP
6. Demo
7. Report

## Reference material
- [DTN](https://en.wikipedia.org/wiki/Delay-tolerant_networking)

