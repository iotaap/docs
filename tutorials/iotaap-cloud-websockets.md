---
title: Websockets
description: 
published: true
date: 2023-06-24T15:20:36.441Z
tags: 
editor: markdown
dateCreated: 2023-06-24T15:20:36.441Z
---

# Websockets

MQTT Websockets are giving you the possibility to access your data using simple, secured websocket interface. 

## Connection

In order to publish and subscribe to your MQTT instance using websockets you have to open a connection. We suggest using 
existing modules or libraries for MQTT WSS, but feel free to use your own implementation. 

| Parameter  |                  Value |
| :--------- | ---------------------: |
| Host       |        network.iotaap.io |
| Port       |                   8084 |
| Path       |                  /mqtt |
| Client ID  |                    any |
| Username   | MQTT instance username |
| Password   | MQTT instance password |
| Keep Alive |                     60 |
| SSL        |                    YES |

> Use the host of your MQTT instance (visible under MQTT Instances in IoTaaP console). MQTT host servers are generated based on the current load of our physical servers. 
{.is-info}


### Example RAW URL

`wss://network.iotaap.io:8084/mqtt`

## Certificate
Device to cloud communication (and vice versa) is fully encrypted with modern encryption technologies. Our servers are containing their certificates (usually valid for 1-2 years, and those are managed by us). Device must contain CA (Certificate Authority) (Root) certificate that is usually valid for 5-10 years. Root certificates are usually installed on your PC, Smartphone, etc. 

Our system is fully protected by Sectigo.

If you think that your system doesn't have the root certificate installed, you can get it [here](/iotaap-os/certificates)