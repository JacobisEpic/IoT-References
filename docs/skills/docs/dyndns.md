# Dynamic DNS

DNS - Domain Name System -- is used to translate host names (e.g.,
whizzer.bu.edu) into IP addresses (e.g., 128.197.53.92). DHCP --
Dynamic Host Configuration Protocol -- is used to dynamically assign an IP
by a host provider to a user device or router. This is to get around
the use of static IP addresses so that the hosting service can reuse
IP addresses that are not currently assigned. For example, Comcast
might use DHCP to assign an IP address to your home router. If the
router is turned off, the IP address can be reallocated to someone
else. You get a new one when your router comes back on line.

Similarly, your home router, and our Linksys router can use their own
DHCP service to generate local IP addresses subservient to the one
assigned by the hosting service (on the "WAN" side of the router). In
most home routers the local addresses are in the 192.168.x.x range, on
the "LAN" side of the router.

Here is where Dynamic DNS (DDNS) comes in. With DHCP assigning IP
addresses willy-nilly, there is no longer a known, fixed IP address
(named or numeric) that we can use to find our device on the
Internet. With DDNS, a host, router, or other device can report its
current IP assignment to a DDNS provider that will keep track of the
assignment and provide a translation of a named address to the dynamic
one. The named address is hosted by the DDNS provider.

All is good except for one more thing. Under this scheme your local
router has a single named DDNS address. We still need to map the WAN
IP address to the LAN addresses. This is achieved by network address
translation (NAT) and port forwarding. Basically one can use port
numbers as a way to distinguish traffic on the local subnet.

For example, we could put a router at 128.197.53.92.  Then on the
router LAN side we have an address range of .1--.255. Suppose the LAN
side has three devices: the router at .1, an ESP at .2, a
web server at .3, and a printer at .4.  We can define specific ports to go
to specific LAN addresses such as:

:1111 traffic --> to the ESP at 192.168.1.2<br>
:2222 traffic --> to the web server at 192.168.1.3<br>
:3333 traffic --> to the printer at 192.168.1.4<br>
All other traffic --> to the router at 192.168.1.1<br>

<p align="center">
<img src="/docs/images/port-forwarding-v2.png" width="100%">
</p>
<p align="center">
<i>Port Forwarding</i>
</p>

So to address the printer we would send to 128.197.53.92:3333. The
router does 'port forwarding' to get the data to the right place. Keep
in mind that many ports are pre-allocated to services such as email,
web traffic, etc. etc. Picking arbitrarily (as done here) will give you
unpredictable results. Check the standard IP port allocations (google) first.

Also, web servers typically listen on port 80 or 8080. If you want web
traffic to get to a specific local address, you might select an
external port such as :1131 mapped to :80. This would look something
like this:

External via DDNS: http://whizzer.bu.edu:1131 --> 
Internal port 192.168.1.3:80

In this exercise you should plan to set up the router to do DDNS and
port forwarding to be able to communicate to and from your device
located on the LAN side of the router. You will need to get a (free)
DDNS account (multiple providers) and set up the router as per the
concepts above.

## Assignment
1. Get a free DDNS account from a provider of your choice (we use Dyn, but any free service is fine)
2. Set up your local router to connect to the DDNS service
3. Setup the RPi or your laptop as a web server (this is the node.js server from previous skill)
4. Demonstrate accessing your web server from the hosted DDNS name (on and off the BU network, e.g., from your cellular service)
5. Report results as usual.

## Reference material
- [DDNS](https://en.wikipedia.org/wiki/Dynamic_DNS)
- [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)
- [Tomato Router](http://www.polarcloud.com/tomato)
- [OpenWRT](https://en.wikipedia.org/wiki/OpenWrt)
