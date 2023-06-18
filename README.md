# aSiNine-ESP-miner (WIP)
Bitcoin miner for BM1387/BM1397 asics on an ESP microcontroller

# (WIP'ing now) Documents first, starting with the built instructions
To compile this software you need

- Arduino IDE (version 1.8.19 or above)
- Support for Espressif ESP's
- Library: PT8211 (see my repositories, extract to your library folder), needed for regulating Vcore with a PT8211s
- Library: WebSerialLite_S9 (see my repositories, extract to your library folder)
- Library: Freenove_WS2812_Lib_for_ESP32 (add with library manager in IDE), needed for the RGB led
- Library: ESPAsyncWebServer (add with library manager in IDE)
- Library: AsyncElegantOTA (add with library manager in IDE)
- Library: ESP32AnalogRead (add with library manager in IDE)
- The contents of this repository, download as zip and extract to your documents/arduino folder.
Compile and upload the sketch to your esp over usb, or when updating the software export the compiled binary so you can update the firmware OTA.

# Manual

## Starting for the first time

The miner will not be configured, so that is the first thing to do to get it up and running. Use a PC with a wireless connection or phone to connect to the miner, it identifies itself as 'ESP miner'. When connected open the miner's webpage at 192.168.4.1

In the bottom field enter

write /wifi.cfg:myssid mypassword

(replace myssid and mypassword with your wifi credentials) and press enter or click on 'Send'. If you are comfortable typing on your current device you can skip rebooting, otherwise type
r
and enter to reboot the miner. When rebooted open the miner's webpage at its new address that can be found in your routers DHCP list. If you skipped rebooting or opened the webpage on its new address continu with configuring the device dependent data;

write /sys.cfg:1397 1 1 1.0

In this example you configure the miner to be using BM1397 asics, 1 in series, 1 parallel (so total asics is 1 x 1 = 1), and the voltage readout needs to be multiplied by 1.0 to get the real value.
Next we will configure the pool the miner will connect to by typing

write /pool.cfg:solo.ckpool.org 3333 1KgwWwBh7qGtcWJ9ZRNTUbVCR1L2qYkzcy pwd MyMiner y

where solo.ckpool.org is the pool address, 3333 is the port number, next is your login name, which is often your BTC address, followed by your password, then the worker name (if the pool does not support worker names enter X) and finally a y or n to indicate if the pool supports custom difficulty settings.
The last configuration is for the asic chips. The easiest way to set these to a 'working' value is by entering

s

which will save the (safe and slow) asic settings as used during bootup of the miner. If you remember previously used settings you can write those to the asic configuration with

write /asic.cfg:300 1350

Where the first number is the frequency in MHz and the second is the core voltage in millivolt. 
You can tune these settings later using f+/f- & v+/v- commands. Now its time for (another) reboot. Enter

r

and the miner will reboot. If the miner will not start mining you can check your configuration files by entering

type filename

where filename is one of the configuration files (don't forget the preceeding '/'). The miner will also report a missing (or very wrong) configuration file at boot up but you will have to open its web page very soon after power up/reboot or you will miss it.
