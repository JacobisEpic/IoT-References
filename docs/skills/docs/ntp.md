# Network Time Protocol

NTP is a handy protocol to synchronize a local machine to special
servers linked to highly accurate UTC. This brings accuracy to within
10's of ms. Once set, an ESP32 can reference it's own timekeeping
until subsequent NTP updates.  We will use SNTP which is a simpler
protocol that does not maintain state.



## Assignment
1. Bring up SNTP for the ESP32
2. Set the local time zone
3. Report.md

## Reference material
- [NTP](https://en.wikipedia.org/wiki/Network_Time_Protocol)
- [SNTP](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sntp)

