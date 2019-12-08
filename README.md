
# SinricPro (ESP8266 / ESP32 SDK)
## Version 2.2.6
## Installation

### VS Code & PlatformIO:
1. Install [VS Code](https://code.visualstudio.com/)  
2. Install [PlatformIO](https://platformio.org/platformio-ide)  
3. Install **SinricPro** library by using [Library Manager](https://docs.platformio.org/en/latest/librarymanager/)  
4. Use included [platformio.ini](https://github.com/sinricpro/esp8266-esp32-sdk/blob/master/pio-examples/switch/platformio.ini) files from [examples](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/pio-examples) to ensure that all dependent libraries will installed automaticly.

![sinricpro library manager](https://raw.githubusercontent.com/sinricpro/images/master/platformio-install-sinricpro.png)

### ArduinoIDE
1. Open Library Manager (*Tools / Manage Libraries*)  
2. Search for *SinricPro* and click *Install*  
3. Repeat step 2 for all [dependent libraries](#dependencies)!
4. Open example in ArduinoIDE (*File / Examples / SinricPro / ...*)  

![ArduinoIDE Library Manager](https://raw.githubusercontent.com/sinricpro/images/master/ArduinoIDE-Library-Manager.png)

---

## Dependencies
[ArduinoJson](https://github.com/bblanchon/ArduinoJson) (Version 6.12.0)   
[WebSocketsClient](https://github.com/Links2004/arduinoWebSockets) (Version 2.2.0)  

---

## Examples
|PlatformIO|Arduino|
|:--:|:--:|
| [Switch](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/pio-examples/switch) |[Switch](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/examples/Switch)|
| [Doorbell](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/pio-examples/doorbell)|[Doorbell](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/examples/doorbell)|
| - | [Lock](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/examples/GarageDoor)|
| [TemperatureSensor](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/pio-examples/temperaturesensor) |[TemperatureSensor](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/examples/temperaturesensor)|
| [TV](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/pio-examples/tv) | [TV](https://github.com/sinricpro/esp8266-esp32-sdk/tree/master/examples/tv)

---

## Usage
#### Include SinricPro-Library (SinricPro.h) and SinricPro-Device-Libraries (eg. SinricProSwitch.h)
```C++
#include <SinricPro.h>
#include <SinricProSwitch.h>
```
#### Define your credentials from SinricPro-Portal (portal.sinric.pro)
```C++
#define APP_KEY    "YOUR-APP-KEY"    // Should look like "de0bxxxx-1x3x-4x3x-ax2x-5dabxxxxxxxx"
#define APP_SECRET "YOUR-APP-SECRET" // Should look like "5f36xxxx-x3x7-4x3x-xexe-e86724a9xxxx-4c4axxxx-3x3x-x5xe-x9x3-333d65xxxxxx"
#define SWITCH_ID  "YOUR-DEVICE-ID"  // Should look like "5dc1564130xxxxxxxxxxxxxx"
```

#### Define callback routine(s)
```C++
bool onPowerState(const String &deviceId, bool &state) {
  Serial.printf("device %s turned %s\r\n", deviceId.c_str(), state?"on":"off");
  return true; // indicate that callback handled correctly
}
```
#### In setup()
```C++
  // create and add a switch to SinricPro
  SinricProSwitch& mySwitch = SinricPro[SWITCH_ID];
  // set callback function
  mySwitch.onPowerState(onPowerState);
  // startup SinricPro
  SinricPro.begin(APP_KEY, APP_SECRET);

```

#### In loop()
```C++
  SinricPro.handle();
```

---
## How to add a device?
Syntax is  
```C++
  DeviceType& myDevice = SinricPro[DEVICE_ID];
```
Example  
```C++
  SinricProSwitch& mySwitch = SinricPro["YOUR-SWITCH-ID-HERE"];
```
*Example 2 (alternatively)*
```C++
  SinricProSwitch& mySwitch = SinricPro.add<SinricProSwitch>("YOUR-SWITCH-ID-HERE");
```

---
## How to retrieve a device for sending an event?
Syntax is  
```C++
  DeviceType& myDevice = SinricPro[DEVICE_ID];
```
Example 1
```C++
  SinricProDoorbell& myDoorbell = SinricPro["YOUR-DOORBELL-ID-HERE"];
  myDoorbell.sendDoorbellEvent();
```

*Example 2 (alternatively)*
```C++
  SinricPro["YOUR-DOORBELL-ID-HERE"].as<SinricProDoorbell>().sendDoorbellEvent();
```


---

# Devices
* Switch
* Dimmable Switch
* Light
* TV
* Speaker
* Thermostat
* Fan (US and non US version)
* Lock
* Doorbell
* Temperaturesensor
* Motionsensor
* Contactsensor
* Windows Air Conditioner

---

# Full user documentation
Please see full user documentation here https://sinricpro.github.io/esp8266-esp32-sdk

