---
title: Configuration wizard
description: 
published: true
date: 2023-06-24T11:45:41.051Z
tags: 
editor: markdown
dateCreated: 2023-06-23T15:41:16.215Z
---

# Configuration Wizard

Configuration Wizard is advanced feature used for parameter configuration via Serial interface. All parameters from default.cfg can be configured by using the following command:

  - **set-system** - wizard to set all parameters from system configuration data
  
  > For easier configuration, that doesn't require serial connection or terminal, we recommend using [IoTaaP OS Web configurator](/iotaap-os/web-configurator).
{.is-info}


## Using commands
Simply type `set-system` command into your serial interface. Wizard will start with the following output:

```
Parameter wizard (leave empty for unchanged):

 String "device_id":5e4ecffe0ed7ef34c0e0ede3
    New "device_id":

```

you can use your serial interface to change the parameter or press **ENTER** to keep the current value. If you want to update a specific parameter,
just enter new value into your serial interface and press **ENTER**, after that you should get the following output (e.g. for auto_update parameter):

```
Boolean "auto_update":true
    New "auto_update":false
--> New "auto_update":false

```

at the end, wizard will automatically exit with the following message:

```
Leaving IoTaaP Configurator (data is saved)

```