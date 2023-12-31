---
title: Publishing the Library
description: 
published: true
date: 2023-06-27T08:49:27.872Z
tags: 
editor: markdown
dateCreated: 2023-06-23T15:55:50.400Z
---

# Publishing IoTaaP OS Library
Since this library was built using PlatformIO we are using `pio` for publishing this library to the PlatformIO registry.

## Versioning
This library uses semantic versioning. Before building procedure library version in `library.json` must be updated. 

CHANGELOG must be also updated by describing changes. 

Finally, in `iotaap_os\src\system\definitions.h` parameter `LIB_VERSION` has to be updated.

## Publishing library to the PlatformIO registry
1. Position your terminal to `iotaap_os` directory (where *library.json* is located)
2. Login to the PlatformIO account using the following command: `pio account login` 
3. Use your PlatformIO credentials to login
4. Execute the following command: `pio pkg publish ./<your-build-tar.gz> --owner=iotaap`

> Please note that only **IoTaaP** organisation member can publish to the registry. Repository owner can add you to the organisation if needed. 
{.is-info}

[![PlatformIO Registry](https://badges.registry.platformio.org/packages/iotaap/library/IoTaaP%20OS.svg)](https://registry.platformio.org/libraries/iotaap/IoTaaP%20OS)