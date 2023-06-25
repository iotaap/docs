---
title: Heartbeat
description: 
published: true
date: 2023-06-25T17:06:31.049Z
tags: 
editor: markdown
dateCreated: 2023-06-25T17:06:31.049Z
---

# Heartbeat service
This service publishes timestamp every 1 second, so your edge device can get synchronized with the server.

## Topic
Once you enable this service in IoTaaP console, you can subscribe to the topic:
`/iotaapsys/services/heartbeat`

## Content
Each second you will receive a message of the following content:

```JSON
{
  "epoch_s": 1687712751,
  "epoch_ms": 1687712751225,
  "timestamp": "2023-06-25 17:05:51"
}
```

