# MQTT5 Recipe

This recipe is supported by the example code found in the course repo
for MQTT version 5 (MQTT5). Valid as of 2023-12-14 under the current
MQTT5, Node.js, and ESP-IDF versions.

## Demo Application

This application sends a value from the ESP32 to a broker. Then the node
app reads the broker and responds to each published item by publishing something
for the ESP32. This app is using MQTT5. 

### Setup steps (our pi is on the local router at `192.168.1.44`)

1. Setup mqqt for ESP32
    -  `idf.py menuconfig`
    - In menuconfig
        - Component config
            - ESP-MQTT Configuration: Select `Enable MQTT protocol 5.0`
        - Example configuration
            - Change mqtt url: `mqtt//:192.168.1.44`
        - Setup Wifi SSID and PWD for your router
2. Build and flash (`idf.py flash`)
3. Install mosquitto on pi
    - ssh into pi (`ssh pi@192.168.1.44`)
    - `sudo apt install -y mosquitto mosquitto-clients`
    - Edit config file `/etc/mosquito/mosquito.conf` and add
```
	listener 1883
        allow_anonymous true
```
4. Install node on the pi (at `192.168.1.44`)

```
wget https://unofficial-builds.nodejs.org/download/release/v20.7.0/node-v20.7.0-linux-armv6l.tar.gz tar -xzf node-v20.7.0-linux-armv6l.tar.gz cd node-v20.7.0-linux-armv6l sudo cp -R * /usr/local
```

5. Install mqtt in your working folder (`/home/pi`)

`npm install mqtt`

6. Transfer node app to the pi (same working folder) ours is called `mqtt5.js`
    - From laptop: `sudo scp ./mqtt.js pi@192.168.1.44:/home/pi`
7. Start mqtt with `mosquitto -v`
8. Start node with `node mqtt5.js`
9. Make sure your ESP32 is transmitting



