# Design Pattern – Setting Real Time on ESP32

One way to obtain real time is to query a Network Time Protocol
server. This networking protocol lets you synchronize your ESP32 to
the same clock source over the internet (requires internet
connectivity). The are other ways to obtain real-time, such syncing
with GPS.

The
[example](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sntp)
from espressif in your esp-idf folder is very extensive on how to
obtain and use real time form the network using Simple-NTP
(SNTP). Worthy a mention is that SNTP is not as accurate as NTP but is
usually sufficient for embedded systems applications. You must also
configure WiFi on your ESP32 by running `idf.py menuconfig` and
provide your WiFi credentials


## References
- [NTP](http://www.ntp.org/ntpfaq/NTP-s-def.htm)
- [SNTP Example Code](https://github.com/espressif/esp-idf/tree/master/examples/protocols/sntp)
- [ESP IDF SNTP](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/kconfig.html?highlight=sntp#sntp)
