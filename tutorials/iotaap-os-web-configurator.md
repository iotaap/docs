---
title: Web Configurator
description: 
published: true
date: 2023-06-24T14:50:18.360Z
tags: 
editor: markdown
dateCreated: 2023-06-24T14:50:18.360Z
---

# IoTaaP OS Web Configurator

IoTaaP OS Web Configurator is an amazing feature that gives you the possibility to configure your **ESP32** based device
without cables, serial port connections and similar.

## Entering IoTaaP OS Web Configurator

During operation or boot, you have to press the predefined “Config button” on the board (routed to GPIO 25) - *please note that IoTaaP OS uses inverted logic, so 10k pull-up resistor to 3.3V is required, and configuration button is active low* 

By pressing "Config button" device will enter into Access Point (AP) mode and start the configurator. 

In the future, every device provided by us will come with a printed SSID and Password, but in order to find your device access data, you can get the SSID and Password of your device during boot (after pressing config button) through the serial port. 

![web-configurator-credentials.png](/tutorials/web-configurator-credentials.png)

During Web configurator operation, onboard LED will blink in a predefined pattern.

![alt text](https://community.iotaap.io/uploads/default/original/1X/a9f746e3c0fdf96fcd19348929f8d6a9a4e15635.png "IoTaaP OS Access Point")

## Opening Web Configurator

Connect to your IoTaaP SSID and head to http://192.168.1.8, this will open the IoTaaP Web configurator:

![iotaap_web_configurator.png](/assets/iotaap_web_configurator.png)

Enter your parameters from the IoTaaP Console, click **Confirm**, and your device will automatically restart and start operating with the new configuration.

## CA certificate

You can get the certificate [here](/iotaap-os/certificates).