---
title: Storing data using Storage service
description: 
published: true
date: 2023-06-27T08:16:35.519Z
tags: 
editor: markdown
dateCreated: 2023-06-27T08:10:38.448Z
---

# Storing data using IoTaaP Storage service
In this tutorial we will write a simple code that will read temperature from [BME280 sensor](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/), and store this temperature to IoTaaP Storage service.

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

  // Store temperature reading to IoTaaP Storage service, and subscribe to callback topic
  iotaapOs.storageServiceStore(TOKEN, "temperature", temperatureC, "/pgiIzx7n/storage/response");

  delay(5000);
}
```

This function is repeated constantly, and it will read the temperature from our BME280 sensor and store it in `temperatureC` variable. Next, we will use `iotaapOs.storageServiceStore()` function to store our reading to the IoTaaP Storage. 

> Do not forget to **update your token** and **update your callbackTopic**. Also your must have permission to listen on your callback topic.
{.is-info}

## Reading from IoTaaP Storage
We will use Postman to read from IoTaaP Storage. This step is described in detail [**here**](https://docs.iotaap.io/en/services/storage-service#retrieving-data).

After populating some data from our sensor, we will get the following response:

```JSON
{
    "data": [
        {
            "time": "2023-06-27T18:14:20.364Z",
            "value": 26.32
        },
        {
            "time": "2023-06-27T18:14:25.364Z",
            "value": 27.32
        },
        {
            "time": "2023-06-27T18:14:30.364Z",
            "value": 28.14
        }
    ]
}
```

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

  // Store temperature reading to IoTaaP Storage service, and subscribe to callback topic
  iotaapOs.storageServiceStore(TOKEN, "temperature", temperatureC, "/pgiIzx7n/storage/response");

  delay(5000);
}
```

> If you have any issues with your code, write to us on our community: [community.iotaap.io](https://community.iotaap.io/)
> 
