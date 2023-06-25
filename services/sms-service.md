---
title: SMS Service
description: 
published: true
date: 2023-06-25T18:02:56.882Z
tags: 
editor: markdown
dateCreated: 2023-06-25T18:02:56.882Z
---

# SMS Module
The Network to SMS module is a valuable component of the IoTaaP Network, enabling devices and applications to send SMS messages using their authentication code. This feature allows seamless SMS communication for all devices on the IoTaaP network, even those without built-in SMS capabilities.

## Sending SMS
In this example we will use third party MQTT Client tool. We will connect to `network.iotaap.io` with our Network Credentials from IoTaaP Console. 

**Service topic**: `/iotaapsys/services/mqttsms`

**Message content:**
```JSON
{
    "token":"qW3LuqeLcq42cBFb-2DtPKiNl47cc97fb394a1447cbbd5e10d1a80851-32d",
    "receiver":"+385917851411",
    "content": "Hello from IoTaaP SMS service.",
    "callbackTopic": "/pgiIzx7n/smsservice/response"
}
```
We have to send a few parameters to this service in order to send SMS:
- **token** - your IoTaaP Link Secret 
- **receiver** - receivers phone number **including** country code
- **content** - content of your SMS message
- **callbackTopic** - (optional) topic for listening to responses from the service

> Please note that **content** maximum length is **120 characters**, and if your message is longer than 120 characters, it will be automatically reduced to 120 characters.
{.is-warning}

Before publishing our message to the SMS service, we will subscribe to our callback topic. 

> Please note that you have to be the owner of callback topic root credential (Network Credential) user.
{.is-warning}

After publishing our message, we will receive response from the server:

![sending-sms-iotaap.png](/assets/sending-sms-iotaap.png)

If error happens during this operation you will receive the response to your callback topic. One of the possible responses is:

```JSON
{
  "error": "Token invalid!"
}
```

**Received SMS** 
In a few seconds we will receive an SMS on our mobile phone:

![received-sms-message.jpeg](/assets/received-sms-message.jpeg)