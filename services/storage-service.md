---
title: Storage service
description: 
published: true
date: 2023-07-05T13:48:26.247Z
tags: 
editor: markdown
dateCreated: 2023-06-25T18:06:29.790Z
---

# Storage Module
This module enables every device or data stream to simply send structured messages to the specific topic and store data to the cloud. With this module, edge devices that are often storage limited can now use practically unlimited server space to store their logs, data, configuration or any other data stream, without need for integration of additional services.

## Storing data
After enabling Storage service in your IoTaaP console, we will connect to the IoTaaP Network using 3rd party MQTT Client tool. In other tutorials, we will be using ESP32 and other solutions to store real data from real devices. 

**Storage service topic**: `/iotaapsys/services/storage/store`

In order to store your data, you will have to publish specific JSON message to Storage service topic over IoTaaP Network.

**Data storage message**:
```JSON
{
    "token":"5gZVuqeLcq42cBFb-4DtPKiNl47cc97fb394a1447cbbd5e10d1a80854-2aa",
    "device": "6475d98175ef35ab92515b28",
    "name":"temperature",
    "value": 29.55,
    "timestamp": 1687704189594,
    "callbackTopic": "/pgiIzx7n/storage/response"
}
```

**Parameters**:
- **token** - your IoTaaP Link Secret
- **device** - your device ID from IoTaaP Console
- **name** - name of your parameter 
- **value** - value of your parameter (**only numeric**)
- **timestamp** - current **UNIX time** in **ms**
- **callbackTopic** - (optional) topic where you will receive response from the service


After publishing our message, on our callback topic we will receive:
```JSON
{
  "status": "success"
}
```
that means that our data is successfully stored. For this example we will publish 3 more values, just by incrementing our timestamp and changing value.

## Retrieving data
Data from IoTaaP Storage can be retrieved by using REST API endpoint, and it can be filtered using basic query parameters.


> Please note that in IoTaaP Storage Basic your **data point** is stored for 6 months. Please contact us for longer storage periods.
{.is-warning}

**Endpoint (GET)**: `https://storage.iotaap.io/v1/list`

**Headers:**
- **secret** - your IoTaaP Link Private token

**Query parameters**:
- **range** - starting point in time for retreiving your data
- **name** - name of the parameter
- **device** - device ID
- **format** - (optional) response format (**csv** / **json**)

> Please note that **range** parameter has to be negative (**TIME NOW (-range)**), since data is retreived **range** units in the past up to the **newest** point record. Range can be in **seconds**, **minutes**, **hours**, **days** and **years** (e.g. **-2s**, **-5m**, **-10h**, **-6d**, **-1y**).
{.is-info}

> If **range** parameter is not provided, default value is **-1h**.
{.is-warning}


In this example our endpoint will be: `https://storage.iotaap.io/v1/list?range=-1h&measurements=temperature,humidity&device=649ff245512f9ecbee9efe03`

It will retreive all data points from **-1h (Latest record time -1 hour)**, and response will be:

```JSON
{
    "humidity": [
        {
            "time": "2023-07-05T12:38:35.328Z",
            "value": 20
        },
        {
            "time": "2023-07-05T12:39:05.376Z",
            "value": 20
        },
        {
            "time": "2023-07-05T12:39:35.423Z",
            "value": 20
        }
    ],
    "temperature": [
        {
            "time": "2023-07-05T12:38:35.328Z",
            "value": -8.199999809
        },
        {
            "time": "2023-07-05T12:39:05.376Z",
            "value": -8.199999809
        },
        {
            "time": "2023-07-05T12:39:35.423Z",
            "value": -9.600000381
        }
    ]
}
```
Each measurement is an array of time and value.

## CSV 
In order to retreive CSV response, we have to add `format=csv` in our query parameters. Our call in this example will be: `https://storage.iotaap.io/v1/list?range=-1h&measurements=temperature,humidity&device=649ff245512f9ecbee9efe03&format=csv`

It will retreive all data points from **-1h (Latest record time -1 hour)**, and response will be:

```csv
time, humidity, temperature
2023-07-05T12:38:35.328Z, 20, -8.199999809
2023-07-05T12:39:05.376Z, 20, -8.199999809
2023-07-05T12:39:35.423Z, 20, -9.600000381
```

### Response headers
`'Content-Type', 'text/csv'`
`'Content-Disposition', 'attachment; filename=data.csv'`

You can handle further processing of this response on your frontend or other application.

## Possible issues
If there is no data, you will receive empty JSON response:

```JSON
{}
```

If your **range** is wrong, you will receive the following response:
```JSON
{
    "message": "Wronq query!"
}
```

If you are not the owner of the device, you will receive the following response:
```JSON
{
    "message": "You are not device owner!"
}
```

If your IoTaaP Link Secret is wrong, you will receive the following response:
```JSON
{
    "message": "IoTaaP secret key not found"
}
```
