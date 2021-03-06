# ANAVI Fume Extractor

**An ESP8266-powered, open source, Wi-Fi dev board for smoke absorber**

---

# DISCLAIMER

ANAVI, the ANAVI logo and combinations thereof, are registered trademarks of Leon Anavi. Other product names may be trademarks of others and the rights belong to their respective owners.

The information in this document is provided in connection with Anavi products. No license, express or implied
or otherwise, to any intellectual property right is granted by this document or in connection with the sale of Anavi products.

This work is licensed under the Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0).
this license, visit https://creativecommons.org/licenses/by-sa/4.0/.

ANAVI Fume Extractor hardware design is licensed under a Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0).

The software examples are released under MIT and the rest of the software is available under GPLv3.

It is possible that the pictures in this manual differ from the latest revision of the board.

The product described in this document is subject to continuous development and improvements. All particulars of the product and its use contained in this document are given by Anavi in good faith. However all warranties implied or expressed including but not limited to implied warranties of merchantability or fitness for purpose are excluded. This document is intended only to assist the reader in the use of the product. Anavi shall not be liable for any loss or damage arising from the use of any information in this document or any error or omission in such information or any incorrect use of the product.

This evaluation board/kit is intended for use for engineering development, demonstration, or evaluation purposes only and is not considered by ANAVI to be a finished end-product fit for general consumer use. People handling the product must have electronics training and observe good engineering practice standards. As such, the goods being provided are not intended to be complete in terms of required design-, marketing-, and/or manufacturing-related protective considerations, including product safety and environmental measures typically found in end products that incorporate such semiconductor components or circuit boards.

There is no warranty for the design materials and the components used to create ANAVI Fume Extractor. There are considered suitable only for ANAVI Fume Extractor.

---

# CHAPTER 1: Overview

## Introduction

ANAVI Fume Extractor is an open source hardware, easy-to-use, Wi-Fi compatible development board for smart smoke absorber for makers. It is powered by ESP8266 and supports 5V 80mm fan, mini OLED display, 5V analog MQ gas sensor and up to 3 additional I2C sensor modules. 

Dangerous fumes during soldering and air pollution is a very serious problem. Monitoring air quality and detecting toxic gases can improve one's quality of life. All these features make ANAVI Fume Extractor appropriate for developers, makers, students and open source enthusiasts who are interested in home automation and an environmentally friendly lifestyle.

ANAVI Fume Extractor is designed with the free and open source electronics design automation suite [KiCAD](http://kicad-pcb.org/). No soldering is required. You can assemble ANAVI Fume Extractor with your bare hands and a screwdriver.

## Features & Specifications

* **CPU:** Tensilica L106 32-bit processor (ESP8266)
* **Connectivity:** Wi-Fi 802.11 b/g/n
* **Gas sensor support:** MQ-135 for air quality or any other 5 V MQ analog gas sensor
* **Peripherals:** 80x80mm 5V fan, mini OLED display, UART pins for flashing custom firmware, button, three slots for I²C sensors
* **Compatibility:** Arduino IDE, PlatformIO, Home Assistant, OpenHAB MQTT, and any modern web browser
* **Certification:** Open Source Hardware Association (OSHWA)
* **Dimensions:** 75 mm x 40 mm

## Target Market

ANAVI Fume Extractor is easy to use. You don’t need to be a tech whiz to use it. You can assemble it without any tools, and only a screwdriver is needed to mount the fan and the OLED display to the acrylic enclosure. Whether you're a newbie to home automation or a skilled engineer, ANAVI Fume Extractor is a great choice for many projects.

ANAVI Fume Extractor can also serve as a convenient development board for home automation. The additional slots for I²C sensor modules makes it suitable for anyone interested in Internet of Things, coding, or open source.

ANAVI Fume Extractor is fully compliant with **Arduino IDE**, **PlatformIO**, the popular open source home automation software platforms **Home Assistant** and **OpenHAB** via the lightweight messaging protocol **MQTT**. With ANAVI Fume Extractor, it is easy for developers to focus on the software by easily building and flashing their own versions of the source code. Tech-savvy users can easily integrate ANAVI Fume Extractor in their existing open source home automation platforms.

## Board Version

Revision 1.1 of ANAVI Fume Extractor was used while writing this document. It is possible that it is outdated so it is always recommended to check the latest sources from the GitHub page of the board.

# CHAPTER 2: Getting Started

## Electrostatic Warning

ANAVI Fume Extractor is shipped in a protective bag. It must **NOT** be exposed to high electrostatic potentials. A grounding strap or similar protective device should be worn when handling the board. Avoid touching the component pins or any other metallic element.

## Requirements

In order to setup ANAVI Fume Extractor the following items are required:

* 5V power supply with microUSB

It is recommended to use 1A (1000mA) or higher power supply.

## Supported Peripherals

ANAVI Fume Extractor has a slot for analog 5V MQ sensor module (MQ-135, MQ-2, MQ-3, MQ-7, etc.), I2C slot for mini OLED display as well as up to 3 slots I2C sensors.

### Sensors

ANAVI Fume Extractor supports 5V analog MQ sensor modules. The additional officially supported I2C add-on sensor modules are for:

* Temperature and humidity (HTU21D)
* Temperature and barometric pressure (BMP180)
* Light (BH1750)
* Color and gesture recognition (APDS-9960)

You may also attach any other I2C sensors but you will have to take care of their software integration.

#### Light Sensor

The official light I2C sensor for ANAVI Fume Extractor is BH1750.

Using 4 Dupont jumper wires connect BH1750 to one of the 3 I2C slots on ANAVI Fume Extractor as follows:

| BH1750   | ANAVI Fume Extractor |
| -------- |:-------------- |
| VCC      | 3.3V           |
| GND      | GND            |
| SCL      | SCL            |
| SDA      | SDA            |


#### I2C External Temperature & Humidity Sensor

The official external temperature and humidity add-on sensor for ANAVI Fume Extractor is HTU21 (SHT21). This is I2C sensor capable of measuring both humidity and temperature.

Using 4 Dupont jumper wires connect HTU21 to one of the 3 I2C slots on ANAVI Fume Extractor as follows:

| HTU21    | ANAVI Fume Extractor |
| -------- |:-------------- |
| VIN      | 3.3V           |
| GND      | GND            |
| SCL      | SCL            |
| SDA      | SDA            |

#### Color & Gesture Recognition Sensor

The official I2C sensor for RGB color and gesture detection is APDS-9960.

Using 4 Dupont jumper wires connect APDS-9960 to one of the 3 I2C slots on ANAVI Fume Extractor as follows:

| APDS-9960  | ANAVI Fume Extractor |
| ---------- |:-------------- |
| VIN        | 3.3V           |
| GND        | GND            |
| SCL        | SCL            |
| SDA        | SDA            |

#### Temperature & Barometric Pressure Sensor

The official temperature and barometric pressure sensor for ANAVI Fume Extractor is BMP180. This is I2C sensor capable of measuring both temperature and barometric pressure.

Using 4 Dupont jumper wires connect BMP180 to one of the 3 I2C slots on ANAVI Fume Extractor as follows:

| BMP180   | ANAVI Fume Extractor |
| -------- |:-------------- |
| VIN      | 3.3V           |
| GND      | GND            |
| SCL      | SCL            |
| SDA      | SDA            |

## Assembly

You can assemble ANAVI Fume Extractor with your bare hands and a screw driver following the steps below:

* Add sensors to your ANAVI Fume Extractor.
* Optionally, you may also assemble the simple acrylic case by removing the protective film and mounting screws.
* Use 5V power supply and plug an appropriate cable in the microUSB of ANAVI Fume Extractor to turn on the board.

## Powering ANAVI Fume Extractor

ANAVI Fume Extractor has been tested using various 5V power supplies and USB to microUSB cables. It is recommended to use 5V power supply with 1A or higher current output. Make sure that you are using a 5V power supply from a trusted supplier. Cheap, untested power supplies can be risky and unreliable.

## Configure ANAVI Fume Extractor

[Video tutorial for getting started with ANAVI Light Controller, same procedure for ANAVI Fume Extractor](https://www.youtube.com/watch?v=Y_81CuuGm0Y)

Turn on ANAVI Fume Extractor by plugging an appropriate power supply. As soon as the board is turned on for the very first time it will create a temporary WiFi access point. Connect to it from your computer, smartphone or tablet.

The default software of ANAVI Fume Extractor has a captive portal which guides you through the configurations. As you see in the video you have to select your WiFi network and enter a password if it is not open.

Our open source software relies on the machine to machine communication protocol MQTT to report data from the sensors. You can connect to your own MQTT broker or just leave the default configurations and connect to the public broker as shown in the video.

It very important to copy the machine ID. Later it is needed to identify your device.

When you are ready just click save. If you have entered valid credentials in a moment ANAVI Fume Extractor will connect to your WiFi network and the configured MQTT broker. This way the configuration is complete and ANAVI Fume Extractor will turn off its temporary WiFi access point. After that your device, for example smartphone as in the video, will automatically connect again to your WiFi network.

To verify that ANAVI Fume Extractor is up and running open a modern web browser and visit demo.anavi.technology. Enter your machine ID. Check the advanced settings only if you are not using the default public MQTT broker. Click connect.

## Reset to Factory Defaults

If you decide to change the settings of ANAVI Fume Extractor you need to reset the board and configure it again.

To reset ANAVI Fume Extractor press the button and hold it for 10 seconds until the red light is blinking. After resetting the board there will be a steady red light that indicates that the temporary WiFi access point is on and you can proceed with the configuration again.

---

# CHAPTER 3: Software Development

## Default Firmware

By default ANAVI Fume Extractor comes with [this free and open source Arduino sketch](https://github.com/AnaviTechnology/anavi-fume-extactor-sw).

## USB to UART Module

For uploading firmware to ANAVI Fume Extractor you need USB to UART module. All kits include CP2102 which out of the box on GNU/Linux distributions. Drivers for MS Windows and Mac OS X are [available at silabs.com](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers).

## Setting up the Arduino IDE

1. Install the Arduino IDE following the instructions from from https://www.arduino.cc/en/Main/Software

2. Add the ESP8266 board package: In **File > Preferences** input http://arduino.esp8266.com/stable/package_esp8266com_index.json into the Additional Board Manager URLs field.

3. In **Tools > Board ... > Boards manager** find and add the **ESP8266** package. Now "Generic ESP8266" should be an option in the **Tools > Boards** menu.

4. In **Tools > Flash Size:** select **4M (1M SPIFFS)**

5. Go to **Sketch > Include Library > Manage Libraries...** and include the following dependencies of the default firmware for ANAVI Fume Extractor:

* WiFiManager by tzapu (version 0.12.0)
* ArduinoJson by Benoit Blanchon (version 5.11.1)
* PubSubClient by Nick O'Leary (version 2.7.0)
* Adafruit HTU21DF Library by Adafruit (version 1.0.1)
* Adafruit APDS9960 Library by Adafruit (version 1.0.5)
* DHT sensor library by Adafruit (version 1.3.4)
* U8g2 by oliver (version 2.23.18)
* OneWire (version 2.3.4)
* DallasTemperature (version 3.8.0)
* Adafruit Unified Sensor by Adafruit (version 1.0.2)
* Adafruit BMP085 Unified by Adafruit (version 1.0.0)


*Note: Issues might be experienced if using different versions of the libraries.*

## Flashing Custom Firmware

Follow the steps below to compile and flash custom firmware on ANAVI Fume Extractor from Arduino IDE:

1. To flash the firmware from Arduino IDE select Tools > Generic ESP8266 Module (Flash mode: DIO, Flash frequency: 40MHz, CPU frequency: 80MHz, Flash size: 4M, Debug port: Disabled, Debug level: None, Reset method: ck, Upload speed: 115200, Port: /dev/ttyUSB0). Set the flash size to 4M (1M SPIFFS). You might need to adjust the port if your USB to serial debug cable is connected on a different port.

2. After that press load an Arduino sketch. [A simple blinking LED example is available at GitHub](https://github.com/AnaviTechnology/anavi-examples/blob/master/anavi-light-controller/anavi-blinking-led/anavi-blinking-led.ino)

3. In Arudino IDE click Verify/Compile (Ctrl+R)

4. Connect ANAVI Fume Extractor to the USB to serial debug board: GND to GND, TX cable to RX of ANAVI Fume Extractor and RX cable to TX of ANAVI Fume Extractor.

5. In Arudino IDE click Upload (Ctrl+U)

6. Press and **hold** the RESET button on ANAVI Fume Extractor. Plug the 5V power supply in the jack of ANAVI Fume Extractor (without releasing the RESET button).

7. In Arduino IDE verify that the upload has been started. Hold RESET until the upload completes.

The output in Arduino IDE for successful flashing is:

```
Archiving built core (caching) in: /tmp/arduino_cache_954939/core/core_esp8266_esp8266_generic_CpuFrequency_80,FlashFreq_40,FlashMode_dio,UploadSpeed_115200,FlashSize_512K64,ResetMethod_ck,Debug_Disabled,DebugLevel_None_____1c2aa2b3da66da225b39c9bfab6531e5.a
Sketch uses 224949 bytes (51%) of program storage space. Maximum is 434160 bytes.
Global variables use 31756 bytes (38%) of dynamic memory, leaving 50164 bytes for local variables. Maximum is 81920 bytes.
Uploading 229104 bytes from /tmp/arduino_build_904122/anavi-blinking-led.ino.bin to flash at 0x00000000
................................................................................ [ 35% ]
................................................................................ [ 71% ]
................................................................                 [ 100% ]
```

If you have flashed the blinking LED example, D1 on ANAVI Fume Extractor with start blinking.

Please have a look at [the YouTube video that shows the exact steps for compiling and uploading an Arduino sketch to a similar of our boards](https://www.youtube.com/watch?v=HMIkPuz0ZJs).

**Note:** you have to be quick between step 5 and 6. Remember to press and **hold** SW1 until the upload completes.

# OTA Firmware Upgrade
Recent versions of the official firmware also support OTA firmware updates by putting a firmare binary on a web server and then triggering the update via a MQTT message. This can be very convenient, as you do not have to connect the device to your computer.

## Check support
If you are unsure if your current firmware supports OTA update, you can first check if your ANAVI Fume Extractor is already setup to receive MQTT commands.

To do this, send a MQTT message to the topic "cmnd/[deviceId]/line1" with message body "test", for example using mosquitto_pub:

```
mosquitto_pub -h [mqttserver] -p 1883 -t cmnd/b5cfb5cfb5cfb5cfb5cfb5cfb5cfb5cf/line1 -u [mqttuser] -P [mqttpass] -m "test"
```

When this message causes the first line of your ANAVI Fume Extractor display to change to "test", OTA updates should be supported.
If not (after double checking that you used the correct topic and deviceId), please first update to a more recent firmware version.

(To reset the line again to the default display, just send an empty message to the same topic).


## Build binary firmware image
Using the arduino build setting above, instead of clicking Upload (Ctrl+U), use Menu Sketch -> Export compiled binary (CTRL+ALT+S). A .bin file will be created in the same folder as the .ino file.
Copy this file to an HTTP webserver, for example a server in your local network.

## Trigger update
The devices listens to MQTT messages in topic "cmnd/[deviceid]/update" and expects messages to be in the format

```
{"file":"/[filePath]", "server": "[server IP or DNS name]"}
```

For example, if you put the file at http://192.168.100.46/anavi.bin:

```
{"file":"/anavi.bin", "server": "192.168.100.46"}
```

If your server does not listen on port 80, you can provide the port, for example for  http://192.168.100.46:8080/anavi.bin:

```
{"file":"/anavi.bin", "server": "192.168.100.46", "port": 8080}
```

Example for sending an update message using mosquitto_pub:

```
mosquitto_pub -h [mqttserver] -p 1883 -t cmnd/b5cfb5cfb5cfb5cfb5cfb5cfb5cfb5cf/update -u [mqttuser] -P [mqttpass] -m "{\"file\":\"anavi.bin\", \"server\":\"192.168.100.46\", \"port\":8080}
```
***Note: To ensure successful update, please specify the file with leading slash ('/'), use an HTTP web server, not HTTPS, and -- when run from the command line -- escape quote characters***

On receipt of this message, ANAVI Fume Extractor will download the file from the specified server, update the firmware and restart. As with the normal firmware update, your saved settings such as WiFi and MQTT server settings should remain as configured.

***Note: After the update, you may find that readings from the DHT22 sensor no longer work and temperature and humidity are shown as "0". In this case, please powercycle the device (unplug power until display turns off, then plug power in again)***


# CHAPTER 4: Home Assistant

[Home Assistant](https://home-assistant.io/) is a free and open-source home automation platform running on Python 3 with more than 1200 components for integration with popular Internet of Things.

ANAVI Fume Extractor can be easily integrated in Home Assistant using the component [MQTT sensor](https://www.home-assistant.io/components/sensor.mqtt/). This component supports JSON in the payload of the MQTT messages. To use, in **configuration.yaml** specify MQTT broker and register the sensor with the correspoding MQTT topic, for example:

* Configure MQTT broker:

```
mqtt:
  broker: 127.0.0.1
```

* Register the MQTT sensor:

```
sensor:
    - platform: mqtt
      name: "Temperature"
      unit_of_measurement: 'C'
      state_topic: "home/room/temperature"
      value_template: "{{value_json.temperature}}"
    - platform: mqtt
      name: "Humidity"
      unit_of_measurement: '%'
      state_topic: "home/room/humidity"
      value_template: "{{value_json.humidity}}"
```

---

# CHAPTER 5: Schematics

## Pinout

The components of ANAVI Fume Extractor relies on ESP8266 (ESP-12 module) and utilizes the following pins:

| Component           | Pins                            |  Arduino Pin ID |
| ------------------- |:------------------------------- |-----------------|
| I2C                 | 13, 14                          |                 |  
| MQ gas sensor       | 2                               | 0 (analog)      |
| Indication LED (D1) | 4                               | 16              |
| Fan On/Off button   | 7                               | 13              |
| Relay               | 6                               | 12              |
| WiFi On/Off Jumper  | 5                               | 14              |
| Reset button (SW1)  | 12                              | 0               |
| Extra GPIO          | 11                              | 2               |
| UART                | 15, 16                          |                 |

## I2C

The sensors that can be connected to ANAVI Fume Extractor communicate with a host microcontroller via a communications standard called **I2C** (Inter-Integrated-Circut). I2C uses two wires, labelled SDA (Serial Data) and SCL (Serial Clock). To function properly, I2C requires a pullup resistor on each of those lines therefore ANAVI Fume Extractor includes two 4.7kohm resistors labelled as R2 and R3. If for one reason or another you need to disable the I2C pullup resistors remove R2 and R3.

---

# CHAPTER 6: Frequently Asked Questions (FAQ)

#### What power supply do I need?

You need a standard 5V power supply with microUSB connector.

#### Why isn't a power supply included?

We were unable to source power supplies with universal plugs for the US/EU/UK at an acceptable. Nowadays, 5V power supplies with a microUSB connector are a commodity item because of most smartphone and tables, so you should be able to easily find a suitable unit online or at your local electronics store.

#### Can I remotely control ANAVI Fume Extractor from a web browser on my smartphone, tablet, or laptop?

Yes, you can use our [demo website](http://demo.anavi.technology/) or easily integrate ANAVI Fume Extractor in your instance of the popular open source platforms [OpenHab 2](https://www.openhab.org/) and [Home Assistant](https://home-assistant.io/) through the protocol MQTT.

#### Is ANAVI Fume Extractor an open source project?

Yes, ANAVI Fume Extractor is an open source hardware project powered and created with free and open source software. The hardware designs are available at [GitHub under CC BY-SA 4.0 license](https://github.com/AnaviTechnology/anavi-fume-extactor). All schematics, documents, and source code files are available at [our GitHub repositories](https://github.com/AnaviTechnology/).

#### Is ANAVI Fume Extractor certified?

ANAVI Fume Extractor is being reviewed by the Open Source Hardware Association.

#### Does ANAVI Fume Extractor use the ESP8266?

Yes, ANAVI Fume Extractor is based on the ESP8266.

#### Can I flash different firmware to ANAVI Fume Extractor?

Yes, using a USB to serial cable, you can flash custom firmware built from your own source code.

#### Is ANAVI Fume Extractor compatible with Arduino IDE?

Yes, ANAVI Fume Extractor is compatible with Arduino IDE. You can easily upload your own Arduino sketches to the board.

#### How can I get involved and help?

Buy any of the available perks, get your hands on the ANAVI Fume Extractor, contribute to our GitHub repositories, and become part of our open source community!


---

# CHAPTER 7: Revision History

## Document Revision

| Date              | Changes                     | Modified pages  | Author          |
| ----------------- |:---------------------------:| :---------------| :---------------|
| 16 November 2019  | Initial release             | All             | Leon Anavi      |

## ANAVI Fume Extractor Revision

| Revision| Notable changes                                              |
| ------- |:-------------------------------------------------------------|
| 1.0     | Stable product                                               |

## See Also

For more information please visit [anavi.technology](http://anavi.technology/) and our [GitHub repositories](https://github.com/AnaviTechnology). If you have any questions or enquiries please contact us through [Facebook](https://www.facebook.com/AnaviTechnology/), [Twitter](https://twitter.com/AnaviTechnology) or [email](mailto:info@anavi.technology).

---
