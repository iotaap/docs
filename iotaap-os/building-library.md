---
title: Building the Library
description: 
published: true
date: 2023-06-23T15:56:33.163Z
tags: 
editor: markdown
dateCreated: 2023-06-23T15:56:33.163Z
---

# Building IoTaaP OS Library
Since this library was built using PlatformIO we are using `pio` for building this library into the package. Library 
as a package can be used for internal projects when library has to be used locally. **This option should be used only
for custom builds.**

## Versioning
This library uses semantic versioning. Before building procedure library version in `library.json` must be updated. 

CHANGELOG.md must be also updated by describing changes. 

Finally, in `iotaap_os\src\system\definitions.h` parameter `LIB_VERSION` has to be updated.

## Building procedure
1. Position your terminal to `iotaap_os` directory (where *library.json* is located)
2. Execute the following command: `pio package pack --output releases/`
3. This command will generate library package in `releases` directory

## CI/CD
CI and CD are handled by internally hosted Jenkins instance. Based on the `Jenkinsfile` new Jenkins Job will be started
on any Pull request (and all checks have to pass before it can be merged with `master` branch) and on every push to any
branch. 