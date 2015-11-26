## esp-dht-transmitter

Software for sending temperature/humidity values over WiFi. Runs on 
ESP8266. Built using Arduino IDE. Supports multiple DHT-22 sensors connected to
different GPIO pins.

Requires [DHT-sensor-library](https://github.com/adafruit/DHT-sensor-library)
and the [ESP8266 Arduino IDE](https://github.com/esp8266/Arduino) extension.

Before opening this in Arduino IDE, create a file `sensor-settings.h` with 
your sensor settings, including Wifi settings. Like this:

```
const char* ssid     = "<my wifi ssid>";
const char* password = "<my wifi password>";

const char* host = "<server ip>";
const int   port = <server port>;

const char* device = "my-esp-transmitter";

#define sensor_count 2
DHT dht[] = { DHT(2, DHT22), DHT(4, DHT22) };

#define DEEP_SLEEP 0   // set to 1 to enable deep sleep
#define SLEEP_SECS 60  // interval between sending

#define TEMP_SEND_THRESHOLD 1.0
#define HUM_SEND_THRESHOLD 1.0
```

Make sure that `sensor_count` matches to the number of sensors defined on the following line, where you define
sensor types and their GPIO pins.

I use my `sensor-server` project as the server that accepts the connections
from my sensors. You may experiment simply with `nc -k -l 5000` as well.
