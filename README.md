# Mortens notes on integration:

## Hardware used:
* The following ESP32 WROOM-32: https://www.aliexpress.com/item/1005005495948290.html?spm=a2g0o.productlist.main.1.3ed4j8YFj8YFeY&algo_pvid=fac508b7-1bfd-4794-9d5e-517e5b5ae8b6&algo_exp_id=fac508b7-1bfd-4794-9d5e-517e5b5ae8b6-0&pdp_npi=4%40dis%21NOK%21267.56%21128.42%21%21%2124.71%21%21%402101ea7116971272833057930e1293%2112000033306300240%21sea%21NO%21139353022%21&curPageLogUid=BKVMPmshX5M0
* Connector:
  * The connector is a PAP-05V-S CONN HOUSING PA 5POS 2MM WHITE (Digi-Key Part Number 455-1489-ND)
  * Used premade pigtail: https://www.aliexpress.com/item/1005002904897793.html?spm=a2g0o.order_list.order_list_main.17.1c711802719bO0
  * The connector is marked with pin 1, and pin 5. The pinout is:
      1. 12V
      2. GND
      3. 5V
      4. TX (Heat pump sends bytes on this pin)
      5. RX (Heat pump receives bytes on this pin)

### Connection made 
Connected to U0-RX and U0-TX, GND and VIN.

## Software used:

Used arduino IDE version 2.2.1

### Libraries used:

* PubSubClient v2.8 
  * Arduino: https://www.arduino.cc/reference/en/libraries/pubsubclient/
  * Author github: https://github.com/knolleary/pubsubclient/tree/v2.8
* SwiCago library:
  * Author github: https://github.com/SwiCago/HeatPump
  * My fork at: https://github.com/molysgaard/HeatPump
  * used revision: cea90c5ed48d24a904835f8918bd88cbc84cb1be
* ArduinoJson 6.21.3
  * Arduino: https://www.arduino.cc/reference/en/libraries/arduinojson/
  * Original github: https://github.com/bblanchon/ArduinoJson/tree/v6.21.3

## Arduino IDE config:
Used board uPesy ESP32 Wroom DevKit from the espressif esp32 board kit

## Configuration
* Hostname: heatpump_living_room
    * Answers to MDNS queries, e.g. `ping heatpump_living_room.local`.

## Physical mounting:
Followed this blog-post about how to install the device inside the heat pump.
https://chrdavis.github.io/hacking-a-mitsubishi-heat-pump-Part-1/

Here is another resource on the connector inside: https://casualhacker.net/post/2017-10-24-CN105_Connector

# mitsubishi2MQTT
Use MQTT and ESP8266/ESP32 module to control Mitsubishi HVAC unit.
It use SwiCago librairies: https://github.com/SwiCago/HeatPump

***
Features:
 - Initial config:  WIFI AP mode and web portal
 - Web interface for configuration, status and control, firmware upgrade
 - Homeassistant autodiscovery and control with MQTT

***
Screenshots:

Main Page
![](https://github.com/gysmo38/mitsubishi2MQTT/blob/master/images/main_page.png)

Control page
![](https://github.com/gysmo38/mitsubishi2MQTT/blob/master/images/control_page.png)

Config page
![](https://github.com/gysmo38/mitsubishi2MQTT/blob/master/images/config_page.png)

***
How to use:
 - Step 1: flash the sketch with flash size include SPIFFS option.
 - Step 2: connect to device AP with name HVAC_XXXX (XXXX last 4 character MAC address)
 - Step 3: You should be automatically redirected to the web portal or go to 192.168.1.1
 - Step 4: set Wifi information, save & reboot. Fall back to AP mode if WiFi connection fails (AP password sets to default SSID name from step 2).
 - Step 5: find the device IP with last 4 character MAC address in your router
 - Step 6: (optional): Set MQTT information for use with Home Assistant
 - Step 7: (optional): Set Login password to prevent unwanted access in SETUP->ADVANCE->Login Password
