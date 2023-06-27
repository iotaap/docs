---
title: Sending SMS with ESP32
description: 
published: true
date: 2023-06-27T08:05:58.103Z
tags: 
editor: markdown
dateCreated: 2023-06-27T08:00:07.802Z
---

# Sending SMS with ESP32 and IoTaaP OS
In this tutorial we will write a simple code that will read temperature from [BME280 sensor](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/), and if temperature is higher than 30°C it will send a SMS to the receivers number.

## platformio.ini 
As usual we will use PlatformIO for this embedded project, and our platformio.ini should look like this:

```
[env:release]
platform = espressif32
board = esp32dev
framework = arduino
monitor_speed = 115200
lib_deps = 
	iotaap/IoTaaP OS@^5.2.2
	adafruit/Adafruit BME280 Library@^2.2.2
board_build.partitions = partitions/default_fat.csv
```

## Headers and declaration

```cpp
#include <IoTaaP_OS.h>
#include <Arduino.h>
#include <ArduinoJson.h>
#include "Adafruit_BME280.h"

#define TOKEN "<iotaap-link-secret>" // IoTaaP Link Secret

Adafruit_BME280 bme;         // I2C
IoTaaP_OS iotaapOs("3.2.8"); // Defining Firmware version
```

We have to include our headers as usual, since Adafruit_BME280.h requires some functions from Arduino.h, we have to include it also. Additionally we have to declare our `bme` sensor and create `iotaapOs` object.

Also we have to define **TOKEN**, so please do not forget to replace `<iotaap-link-secret>` with your IoTaaP Link Secret.

## setup() function

```cpp
void setup()
{
  // BME280 related stuff
  unsigned status;
  status = bme.begin(0x76);
  if (!status)
  {
    Serial.println("Could not find a valid BME280 sensor, check wiring, address, sensor ID!");
    while (1)
      delay(10);
  }

  iotaapOs.start(); // Start IoTaaP OS

  iotaapOs.startWifi();         // Connect to WiFi
  iotaapOs.startMqtt(callback); // Connect to MQTT broker
}
```

In the first part of the function, we are checking if BME280 is available and working, this is a good practice in this example, to eliminate further issues if sensor is not working properly. 

Next, we have to call **iotaapOs.start()** function to start our IoTaaP OS services, this is followed by **iotaapOs.startWifi()** to connect to start WiFi service and **iotaapOs.startMqtt()** to connect to the IoTaaP network, and define MQTT callback function.

## callback() function

```cpp
void callback(char *topic, byte *message, unsigned int length)
{
  Serial.println("-------#-----#-----#----------");
  Serial.println("Received data on the topic:");
  Serial.println(topic); // Print topic

  Serial.println("Data:");

  for (int i = 0; i < length; i++) // Print message
  {
    Serial.print((char)message[i]);
  }
  Serial.println();
  Serial.println("------#------#------#---------");
}
```

This is basic MQTT callback function that will print received data and topic to our Serial Terminal, it is used to check the status of the service.

## loop() function

```cpp
void loop()
{

  // Fetch measurements from BME280 sensor
  float temperatureC = bme.readTemperature();

  // If temperature is higher than 30°C, send SMS using IoTaaP SMS service, and subscribe to callback topic
  if (temperatureC > 30)
  {
    char message[50];
    sprintf(message, "Current temperature is: %.1f°C", temperatureC);
    iotaapOs.smsServiceSend(TOKEN, "+38599", message, "/pgiIzx7n/smsservice/response");
  }

  delay(5000);
}
```

This function is repeated constantly, and it will read the temperature from our BME280 sensor and store it in `temperatureC` variable. Next, we will check if temperature is higher than 30°C and if it is we will first craft our SMS message using `sprintf` function. 

Finally, we will use `iotaapOs.smsServiceSend()` function to send the SMS using IoTaaP SMS service. 

> Do not forget to **update receivers phone number** (it must contain country code). Also your must have permission to listen on your callback topic.
{.is-info}

## Complete code
Below you can find the complete code for this example.

```cpp
#include <IoTaaP_OS.h>
#include <Arduino.h>
#include <ArduinoJson.h>
#include "Adafruit_BME280.h"

#define TOKEN "<iotaap-link-secret>" // IoTaaP Link Secret

Adafruit_BME280 bme;         // I2C
IoTaaP_OS iotaapOs("3.2.8"); // Defining Firmware version

// IoTaaP Network (MQTT) callback function
void callback(char *topic, byte *message, unsigned int length)
{
  Serial.println("-------#-----#-----#----------");
  Serial.println("Received data on the topic:");
  Serial.println(topic); // Print topic

  Serial.println("Data:");

  for (int i = 0; i < length; i++) // Print message
  {
    Serial.print((char)message[i]);
  }
  Serial.println();
  Serial.println("------#------#------#---------");
}

void setup()
{
  // BME280 related stuff
  unsigned status;
  status = bme.begin(0x76);
  if (!status)
  {
    Serial.println("Could not find a valid BME280 sensor, check wiring, address, sensor ID!");
    while (1)
      delay(10);
  }

  iotaapOs.start(); // Start IoTaaP OS

  iotaapOs.startWifi();         // Connect to WiFi
  iotaapOs.startMqtt(callback); // Connect to MQTT broker
}

void loop()
{

  // Fetch measurements from BME280 sensor
  float temperatureC = bme.readTemperature();

  // If temperature is higher than 30°C, send SMS using IoTaaP SMS service, and subscribe to callback topic
  if (temperatureC > 30)
  {
    char message[50];
    sprintf(message, "Current temperature is: %.1f°C", temperatureC);
    iotaapOs.smsServiceSend(TOKEN, "+38599", message, "/pgiIzx7n/smsservice/response");
  }

  delay(5000);
}
```

> If you have any issues with your code, write to us on our community: [community.iotaap.io](https://community.iotaap.io/)
> 
