# Sofar2mqtt - ESP32 fork.
## A smart home interface for Sofar solar and battery inverters.

Supported models:  

ME3000SP - Full support  
HYD-xx00-ES - Full support

![image](https://user-images.githubusercontent.com/43951291/174405916-3ef3bff7-4cb5-4531-b8f7-9626383aeffe.png)

![image](https://user-images.githubusercontent.com/43951291/174405772-b194db91-e26b-4341-960b-4e7e2e368873.png)


Sofar2mqtt is a remote control interface for Sofar solar and battery inverters.
It allows remote control of the inverter and reports the invertor status, power usage, battery state etc for integration with smart home systems such as [Home Assistant](https://www.home-assistant.io/) and [Node-Red](https://nodered.org/).  
For read only mode, it will send status messages without the inverter needing to be in passive mode.  
It's designed to run on an ESP8266 microcontroller with a TTL to RS485 module such as MAX485 or MAX3485.  
Designed to work with TTL modules with or without the DR and RE flow control pins. If your TTL module does not have these pins then just ignore the wire from D5. 

Subscribe your MQTT client to:

Sofar2mqtt/state

Which provides:

running_state  
grid_voltage  
grid_current  
grid_freq  
battery_power  
battery_voltage  
battery_current  
batterySOC  
battery_temp  
battery_cycles  
grid_power  
consumption  
solarPV  
today_generation  
today_exported  
today_purchase  
today_consumption  
inverter_temp  
inverterHS_temp  
solarPVAmps  

With the inverter in Passive Mode, send MQTT messages to:

Sofar2mqtt/set/standby   - send value "true"  
Sofar2mqtt/set/auto   - send value "true" or "battery_save"  
Sofar2mqtt/set/charge   - send values in the range 0-3000 (watts)  
Sofar2mqtt/set/discharge   - send values in the range 0-3000 (watts) 

battery_save is a hybrid auto mode that will charge from excess solar but not discharge.

(c)Colin McGerty 2021 colin@mcgerty.co.uk  
Thanks to Rich Platts for hybrid model code and testing.  
calcCRC by angelo.compagnucci@gmail.com and jpmzometa@gmail.com

# How To Build

Parts List:
1. ESP32 D1 Mini or clone
2. MAX485 or MAX3485 TTL to RS485 board*
3. 0.96" I2C OLED Screen (optional)

*The MAX3485 (which is red, not blue like the MAX485 shown here) is preferred as it is much more stable because it uses 3.3v logic, just like the ESP8366. The MAX485 uses 5v logic but is somewhat tolerant of 3.3v and is generally cheaper and more widely available. I use a MAX485 but many people have reported problems with this and if you can find a MAX3485 then you should use that. MAX3485 boards do not have DR and RE flow control pins, so just skip the wire from pin D5 in the wiring diagram below.

The 3d printable DIN case can be found here:
https://www.thingiverse.com/thing:5413436
