# Security and Privacy in Connected Systems

What is the problem here?  We don't want any of the following to
happen in any system we build using embedded devices:

- An adversary can take control of an embedded device (such as an ESP32)
  - Falsifying sensor data
  - Falsifying control and actuation
- An adversary replaces embedded device with own device, and falsifies data and control
- An adversary listens in or modifies data between embedded device and server ("actor-in-the-middle" or "eavesdrop" attack)
- An adversary takes control of server (local or remote server)
  - And is able  to look at all data from all sensors
  - And is able to control and actuate all devices
- An adversary interrupts flow of information (denial of service -- DOS)
- An adversary physically attacks embedded device or server -- steals one

And what is the nature of the damage? There will be a range of outcomes
- Gain data that provides an advantage (e.g., faster GPS routing of car)
- Learn about when someone is home or not (e.g., robbers); loss of privacy
- Possibly life-critical: overrides safety (causes a fire, causes collision, etc.)
- Economic loss (turn off irrigation, cause crops to fail)


## Assignment

Suppose you are assigned the task of driving your car/robot via remote
control over the internet.  Based on the skills learned in the course,
you should have a sense of what tools and network communication will
be required to do this.

1. Sketch the overall flow of information to drive a car with remote control over the Internet.
2. Identify weaknesses in your overall system (client, local network, internet, server, node.js, ESP32) with respect to security compromise.
3. List at least five ways can a bad guy attack your specific system. Be very specific
4. Describe a way to mitigate each attack
5. Write up your answers and report -- please include graphics as necessary to support your response


## References
- [Mozilla Foundation Investigation of Data Collection by Automakers](https://foundation.mozilla.org/en/privacynotincluded/articles/its-official-cars-are-the-worst-product-category-we-have-ever-reviewed-for-privacy/)
-[Recent EU Legislation on IoT Security](https://www.consilium.europa.eu/en/press/press-releases/2023/11/30/cyber-resilience-act-council-and-parliament-strike-a-deal-on-security-requirements-for-digital-products/)