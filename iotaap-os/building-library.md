---
title: Building the Library
description: 
published: true
date: 2023-06-27T08:45:30.569Z
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

CHANGELOG must be also updated by describing changes. 

Finally, in `iotaap_os\src\system\definitions.h` parameter `LIB_VERSION` has to be updated.

## Building procedure
1. Position your terminal to `iotaap_os` directory (where *library.json* is located)
2. Execute the following command: `pio pkg pack`
3. This command will generate library package in the current directory

## Testing
Testing is handled by GitHub Actions. Based on the `build.yml` new Build will be started on any Pull request (and all checks have to pass before it can be merged with `master` branch).

## Current build status
[![IoTaaP OS Build](https://github.com/iotaap/iotaap-os/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/iotaap/iotaap-os/actions/workflows/build.yml)
