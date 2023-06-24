---
title: IoTaaP Cloud - MQTTS
description: 
published: true
date: 2023-06-24T15:09:52.442Z
tags: 
editor: markdown
dateCreated: 2023-06-24T15:09:52.442Z
---

# IoTaaP Cloud - MQTTS

IoTaaP Cloud gives you everything you need to successfuly manage, update and secure your IoT devices and services. Our **IoTaaP Cloud Console** gives you the possibility to add new devices, make OTA Updates, manage MQTTS instances, develop your IoT solution and finally bring your IoT solution online. 

> Managing your edge device security, maintaining stable connection and doing remote upgrades can be a tough thing to do. Because of the same struggle, we have created our **IoTaaP OS**. Unique Open Source solution built on top of FreeRTOS for ESP32 SoC which provides everything you need to successfully develop, deploy and manage your IoT devices.
{.is-info}


## IoTaaP Console account

In this step we will setup our IoTaaP Console free account for testing. Go to [IoTaaP Console](https://console.iotaap.io/auth/register) and create your account with your e-mail.

### Creating devices and MQTT instances

Video tutorial:

[![IoTaaP Instances](http://img.youtube.com/vi/zupJiFhtNBg/0.jpg)](http://www.youtube.com/watch?v=zupJiFhtNBg "IoTaaP Instances")

## IoTaaP MQTT broker

One of the most crucial IoT parts is the communication channel. One of the most common protocols used for IoT communication is MQTT (Message Queuing Telemetry Transport) which provides lightweight methods of carrying out messaging using publish and subscribe queueing model.

![publisher-subscriber.jpg](/tutorials/publisher-subscriber.jpg)

MQTT is ideal for IoT, it is designed to be minimal and this is perfect to use it in mobility, embedded systems another bandwidth-sensitive application. MQTT introduces something called “MQTT Broker”, this is in the matter of fact the heart of publish/subscribe protocol, like MQTT is.

MQTT broker is responsible for receiving messages, filtering, determining who is subscribed to the message, and sending messages to subscribed clients (devices, phones, applications…) MQTT is based on TCP/IP.

In the steps below we will go through the process of creating your Free MQTT instance using IoTaaP Console and testing it.

## Creating new instance

From the right sidebar select **“MQTT“**. In the MQTT page simply click on the green "+" button, and our system will automatically generate and configure new MQTTS instance for you. 

## Instance Data

If everything went well, you will see your instance up and running. You will be able to see your instance info and parameters that we will use to intereact with your instance.

- **User** will be used to connect with your instance
- **Password** will be used to connect with your instance
- **Server** is the server where you can access your instance
- **Port** is the port where your instance is running

## Testing with MQTT.fx

To test our instance, we will use **MQTT.FX**, this  is a MQTT Client written in Java based on [Eclipse Paho](http://www.eclipse.org/paho/). Download latest release of MQTT.fx from [here](https://mqttfx.jensd.de/index.php/download). Select and download MQTT for your platform (Windows, Linux…). Run your setup and install it. After running MQTT.fx, click on **Edit Connection Profiles**, cog, next to the Connect button.

![alt text](https://files.iotaap.io/assets/iotaap-tutorials/cloudmqtt-setup/iotaap-configure-mqttfx.png"MQTT FX")

This is the place where we will add our new MQTT connection. Simply click on the **+** button in the bottom left corner and fill your new profile with the data from IoTaaP Console MQTT instance info.


**Do not forget to enter your User and Password in “User Credentials” tab!**

> As our IoTaaP MQTT Broker works only with secured connection (MQTTS), we have to configure SSL certificates in order to be able to connect to the server. Simply open SSL/TLS tab and provide the path to our IoTaaP MQTTS Certificate under CA Certificate file. 
{.is-info}


**IoTaaP MQTTS Certificate**

Our system is fully protected by Sectigo.

**Root Certificate**

```
-----BEGIN CERTIFICATE-----
MIIF3jCCA8agAwIBAgIQAf1tMPyjylGoG7xkDjUDLTANBgkqhkiG9w0BAQwFADCB
iDELMAkGA1UEBhMCVVMxEzARBgNVBAgTCk5ldyBKZXJzZXkxFDASBgNVBAcTC0pl
cnNleSBDaXR5MR4wHAYDVQQKExVUaGUgVVNFUlRSVVNUIE5ldHdvcmsxLjAsBgNV
BAMTJVVTRVJUcnVzdCBSU0EgQ2VydGlmaWNhdGlvbiBBdXRob3JpdHkwHhcNMTAw
MjAxMDAwMDAwWhcNMzgwMTE4MjM1OTU5WjCBiDELMAkGA1UEBhMCVVMxEzARBgNV
BAgTCk5ldyBKZXJzZXkxFDASBgNVBAcTC0plcnNleSBDaXR5MR4wHAYDVQQKExVU
aGUgVVNFUlRSVVNUIE5ldHdvcmsxLjAsBgNVBAMTJVVTRVJUcnVzdCBSU0EgQ2Vy
dGlmaWNhdGlvbiBBdXRob3JpdHkwggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIK
AoICAQCAEmUXNg7D2wiz0KxXDXbtzSfTTK1Qg2HiqiBNCS1kCdzOiZ/MPans9s/B
3PHTsdZ7NygRK0faOca8Ohm0X6a9fZ2jY0K2dvKpOyuR+OJv0OwWIJAJPuLodMkY
tJHUYmTbf6MG8YgYapAiPLz+E/CHFHv25B+O1ORRxhFnRghRy4YUVD+8M/5+bJz/
Fp0YvVGONaanZshyZ9shZrHUm3gDwFA66Mzw3LyeTP6vBZY1H1dat//O+T23LLb2
VN3I5xI6Ta5MirdcmrS3ID3KfyI0rn47aGYBROcBTkZTmzNg95S+UzeQc0PzMsNT
79uq/nROacdrjGCT3sTHDN/hMq7MkztReJVni+49Vv4M0GkPGw/zJSZrM233bkf6
c0Plfg6lZrEpfDKEY1WJxA3Bk1QwGROs0303p+tdOmw1XNtB1xLaqUkL39iAigmT
Yo61Zs8liM2EuLE/pDkP2QKe6xJMlXzzawWpXhaDzLhn4ugTncxbgtNMs+1b/97l
c6wjOy0AvzVVdAlJ2ElYGn+SNuZRkg7zJn0cTRe8yexDJtC/QV9AqURE9JnnV4ee
UB9XVKg+/XRjL7FQZQnmWEIuQxpMtPAlR1n6BB6T1CZGSlCBst6+eLf8ZxXhyVeE
Hg9j1uliutZfVS7qXMYoCAQlObgOK6nyTJccBz8NUvXt7y+CDwIDAQABo0IwQDAd
BgNVHQ4EFgQUU3m/WqorSs9UgOHYm8Cd8rIDZsswDgYDVR0PAQH/BAQDAgEGMA8G
A1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQEMBQADggIBAFzUfA3P9wF9QZllDHPF
Up/L+M+ZBn8b2kMVn54CVVeWFPFSPCeHlCjtHzoBN6J2/FNQwISbxmtOuowhT6KO
VWKR82kV2LyI48SqC/3vqOlLVSoGIG1VeCkZ7l8wXEskEVX/JJpuXior7gtNn3/3
ATiUFJVDBwn7YKnuHKsSjKCaXqeYalltiz8I+8jRRa8YFWSQEg9zKC7F4iRO/Fjs
8PRF/iKz6y+O0tlFYQXBl2+odnKPi4w2r78NBc5xjeambx9spnFixdjQg3IM8WcR
iQycE0xyNN+81XHfqnHd4blsjDwSXWXavVcStkNr/+XeTWYRUc+ZruwXtuhxkYze
Sf7dNXGiFSeUHM9h4ya7b6NnJSFd5t0dCy5oGzuCr+yDZ4XUmFF0sbmZgIn/f3gZ
XHlKYC6SQK5MNyosycdiyA5d9zZbyuAlJQG03RoHnHcAP9Dc1ew91Pq7P8yF1m9/
qS3fuQL39ZeatTXaw2ewh0qpKJ4jjv9cJ2vhsE/zB+4ALtRZh8tSQZXq9EfX7mRB
VXyNWQKV3WKdwrnuWih0hKWbt5DHDAff9Yk2dDLWKMGwsAvgnEzDHNb842m1R0aB
L6KCq9NjRHDEjf8tM7qtj3u1cIiuPhnPQCjY/MiQu12ZIvVS5ljFH4gxQ+6IHdfG
jjxDah2nGN59PRbxYvnKkKj9
-----END CERTIFICATE-----
```

[**DOWNLOAD**](/certificates/sha-2_root_usertrust_rsa_certification_authority.crt)

> System will not be able to connect to the MQTT server or do the OTA update if certificate is missing or invalid.
{.is-warning}


Click Apply and close the widow. **Next** is to connect to our MQTT instance, select your instance from the dropdown menu, and click connect.

![alt text](https://files.iotaap.io/assets/iotaap-tutorials/cloudmqtt-setup/mqttfx-ssl-certificate.png"CA Certificate")

In the next step we will publish our first topic!

## Publishing topic

In this step we will publish our first topic.

![alt text](https://files.iotaap.io/assets/iotaap-tutorials/cloudmqtt-setup/mqtt-publis-topic.png"MQTT Publish new topic")

> You can only publish to the topics that begin with your MQTTS instance username (e.g. `/<username>/kitchen/light`). This is the root of every topic, and if you try to publish to a different root topic (that you do not own), MQTTS server will refuse the connection.
{.is-warning}


We have to write our topic and a message. In this example we will sent the `state` of the kitchen light as boolean parameter

``` json
{
	"state": true
}
```

Let’s say that we want to turn on our kitchen light. As you can see we will write **/tiALJgRN/kitchen/light** and this will be our topic, for example **/tiALJgRN/kitchen/fridge** could be our fridge topic.

Important things about MQTT topic names:

**Case sensitive**

**Must start with root topic `/<username>`**

**Use UTF-8 strings**

**Must consist of at least one character to be valid**

> For best performance and in order to enable IoTaaP Console full debugging performance your data should be JSON structured instead of using plain text.
{.is-info}



## Subscribing

Now when we are sure that our connection works and that we can publish, we will subscribe our “client” to the topic.

Open your **MQTT.fx** and select **Subscribe** tab, next to the Publish tab. We will subscribe to our ‘kitchen light’ topic. Write **“/tiALJgRN/kitchen/light”** to the subscribe field and click **Subscribe**. You will see your topic listed.

![alt text](https://files.iotaap.io/assets/iotaap-tutorials/cloudmqtt-setup/mqtt-iot-subsribe-topic.png"MQTT Subscribe")

Next, we will publish to our topic by clicking Publish button on the **Publish** tab. Click back on the **Subscribe** tab, and you will see your topic's data received. Try to change your message data and publish it again, also, you can play by adding various topics (e.g. /garden/fountain/water or /garden/fountain/light).

![alt text](https://files.iotaap.io/assets/iotaap-tutorials/cloudmqtt-setup/mqtt-topic-payload-published.png"MQTT Subscribe topic")