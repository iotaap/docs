---
title: REST service
description: 
published: true
date: 2023-07-05T11:57:52.183Z
tags: 
editor: markdown
dateCreated: 2023-06-25T17:36:07.995Z
---

# REST Service (ReqMQ)
The REST to Network module is a valuable addition to the IoTaaP network, allowing users and applications to send standard REST requests to the server. These requests are then published on the network, enabling data and command transmission from applications to devices using the widely adopted REST protocol. This module enhances interoperability and connectivity by leveraging the familiar REST interface, simplifying integration and enabling seamless communication within the IoTaaP ecosystem.

## Sending request
In this example we will use **Postman** to send POST request to this service endpoint. 

**Endpoint:** `https://reqmq.iotaap.io/v1/publish`

**Headers:**
- **secret** - your IoTaaP Link Private token
- **username** - network user that will publish the message
- **topic** - topic on which message will be published (without root username)

**Body** - whole request body is treated as your message, we recommend using JSON format, although you can send raw values. 

After adding headers, your Postman interface should look similar to this:

![postman-reqmq-headers.png](/assets/postman-reqmq-headers.png)

Under **Body** we will select **raw** and **JSON** format, and our content will be 

```JSON
{
    "message": "Hello IoTaaP!"
}
```

Once we click **Send** button, in **Response** we will get response from IoTaaP Cloud:
```JSON
{
    "message": "Message published"
}
```

For this example we are using **Network Client** in IoTaaP Console to subscribe to our topic, and there we will receive our message:

![iotaap-console-network-client.png](/assets/iotaap-console-network-client.png)