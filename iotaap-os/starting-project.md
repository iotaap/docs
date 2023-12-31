---
title: Starting project
description: 
published: true
date: 2023-06-27T08:50:42.862Z
tags: 
editor: markdown
dateCreated: 2023-06-17T16:40:39.388Z
---

# Starting a new IoTaaP OS project using PlatformIO

We recommend you go through the example project that is available in the examples folder, and in IoTaaP OS [tutorial](https://docs.iotaap.io/en/iotaap-os/Introduction).

## Installing IoTaaP OS using PlatformIO

You have to declare library dependencies in your `platformio.ini` file, by using [lib_deps](https://docs.platformio.org/page/projectconf/section_env_library.html) option. You can define the specific library version, although we recommend using the newest version in your projects.

#### Example project configuration

```
[env:myenv]
platform = espressif32
board = esp32dev
framework = arduino

lib_deps =

     # RECOMMENDED
     # Accept new functionality in a backwards compatible manner and patches
     iotaap/IoTaaP OS @ ^5.0.0

     # Accept only backwards compatible bug fixes
     # (any version with the same major and minor versions, and an equal or greater patch version)
     iotaap/IoTaaP OS @ ~5.0.0

     # The exact version
     iotaap/IoTaaP OS @ 5.0.0

```

More info about Library installation using PlatformIO can be found [here](https://registry.platformio.org/libraries/iotaap/IoTaaP%20OS/installation).