---
title: Remote Flash
description: 
published: true
date: 2023-06-27T08:38:37.312Z
tags: 
editor: markdown
dateCreated: 2023-06-24T15:23:48.623Z
---

# IoTaaP OS Remote flash

Starting from IoTaaP OS version 4, and IoTaaP Cloud version 2, remote flashing option is available. This feature gives you the possibility to remotely flash you **ESP32** device that runs IoTaaP OS. Please note that
you have to flash IoTaaP OS to your device, and configure it using parameters provided in the IoTaaP Cloud console.

### Firmware - firmware.bin

Everything starts with **firmware.bin** file, this file contains your compiled code, it can be some official release of our modules firmware or your custom firmware. It is important that your new firmware
uses IoTaaP OS (latest version is recommended), otherwise you will lose access to your device. 

If you are using some official firmware by IoTaaP (or authorized partners) than you can skip the following steps,
but if you are using your own solution then you first have to compile your code using PlatformIO (which is recommended development framework).

First you have to **Build** your firmware by clicking on the checkmark icon in PlatformIO interface

![compile.png](/tutorials/compile.png)

After successfull compilation, your **firmware.bin** will be available under `.pio/build/release` directory

![firmware_bin.png](/tutorials/firmware_bin.png)

After successfull remote flashing, your device will restart, and you will see new **Firmware version** in the device details.

## Device remote flash

If automatic OTA updates are enabled, your system will check for new updates every 6 hours, this is sometimes good option when you are deploying group updates, or fast reaction is not required. But mostly, 
you will need to push new updates instantly, especially during development, if your device is already installed in some system or similar. 

### Flashing using IoTaaP Cloud Console

Select your device in IoTaaP Console. You will see your device details and MQTTS connection menu, where you have to connect to the **same** MQTTS server as your device. If your device is turned on, you will be able
to see the device status, firmware version and other parameters. 

![device_status.png](/tutorials/device_status.png)

Next, you have to drag and drop your **firmware.bin** to the upload field, and enter your firmware version. **Version should match your version defined in the main code** `IoTaaP_OS iotaapOs("1.0.7");` After uploading, click on the **Submit** button, and your firmware will be ready for flashing.

![firmware_uploaded_device.png](/tutorials/firmware_uploaded_device.png)

You will notice that **Firmware version** field will change color to red, which indicates that firmware on the device is different then the firmware you have uploaded. Click on the **Flash** button, to start the update procedure. 

![flash_button.png](/tutorials/flash_button.png)

## Group remote flash

If you have multiple devices with the same firmware, you can add them to a **Group** and flash thousands of devices at the same time, without cables and programmers. 

### Flashing using IoTaaP Cloud Console

Select your group of devices in the console by clicking on the green action button (Devices List). This will open list of devices that are currently available in your group. In order to start flashing procedure, you have
to connect to the **same** MQTTS server as your device. 

![mqtt_server_connect.png](/tutorials/mqtt_server_connect.png)

Next, drag and drop your **firmware.bin** to the upload field in the console, and enter your firmware version. **Version should match your version defined in the main code** `IoTaaP_OS iotaapOs("1.0.7");` After uploading, click on the **Submit** button, and your firmware will be ready for flashing.

![firmware_uploaded.png](/tutorials/firmware_uploaded.png)

Now you are ready to start your group flashing by clicking on the **Flash** button. Your device will start the update procedure instantly. 

![flash_button.png](/tutorials/flash_button.png)

You can monitor update status, and overall device status in device details interface.

## Firmware version

Please ensure that you enter the same version to the **Version** field in the console, and as fwVersion parameter in your main code. 

Also, after successfull update and restart, at each IoTaaP OS boot, you will be able to see the current firmware version, as well as IoTaaP OS version

![web-configurator-credentials.png](/tutorials/web-configurator-credentials.png)

> Please note that you will not be able to flash single device if it's a part of the group, even if you remove it from the group in the console. Device can be configured as a stand-alone device or as a part of the group. This configuration can be updated using IoTaaP Web Configurator.
{.is-info}
