t# aSiNine-ESP-miner (WIP)
Bitcoin miner for BM1387/BM1397 asics on an ESP microcontroller

# (WIP'ing now) Documents first, starting with the built instructions
To compile this software you need

- Arduino IDE (version 1.8.19 or above)
- Support for Espressif ESP's (https://randomnerdtutorials.com/installing-esp32-arduino-ide-2-0/)
- Library: PT8211 (see my repositories, extract to your library folder), needed for regulating Vcore with a PT8211s
- Library: WebSerialLite_S9 (see my repositories, extract to your library folder)
- Library: Freenove_WS2812_Lib_for_ESP32 ([github, download as zip and extract to your library folder](https://github.com/Freenove/Freenove_WS2812_Lib_for_ESP32)), needed for the RGB led
- Library: ESPAsyncWebServer (add with library manager in IDE)
- Library: AsyncElegantOTA (add with library manager in IDE)
- Library: ESP32AnalogRead (add with library manager in IDE)
- The contents of this repository, download as zip and extract to your documents/arduino folder.
Compile and upload the sketch to your esp over usb, or when updating the software export the compiled binary so you can update the firmware OTA.

# Manual

## Prerequisites

To operate this miner you need a wifi network to connect to, and a suitable power supply (5V,3A) with a USB-C connector.

## Starting for the first time

Connect the power supply. The miner will not be configured, so that is the first thing to do to get it up and running. The miner's led will be red at this point to show it has no wifi connection and has setup an access point. Use a PC with a wireless connection or phone to connect to this access point, it identifies itself as 'aSiNineMiner', and the password is 'bm1387bm1397'. When connected open the miner's webpage at 192.168.4.1

In the bottom field enter

<b>write /wifi.cfg:myssid mypassword</b>

(replace myssid and mypassword with your wifi credentials) and press enter or click on 'Send'. Note that the miner will automatically reboot after 1 minute. Wait for the miner to reboot or type
<b>r</b>
and enter to reboot the miner. The led should no longer be red to signal it has a wifi connection. Open the miner's webpage at its new address that can be found in your routers DHCP list. Now we configure the device dependent data; type

<b>write /sys.cfg:1397 1 1 1.0</b>

In this example you configure the miner to be using BM1397 asics, 1 in series, 1 parallel (so total asics is 1 x 1 = 1), and the voltage readout needs to be multiplied by 1.0 to get the real value. Warning: by entering wrong values here you can physsically damage the miner!
Next we will configure the pool the miner will connect to by typing

<b>write /pool.cfg:solo.ckpool.org 3333 1KgwWwBh7qGtcWJ9ZRNTUbVCR1L2qYkzcy pwd MyMiner y</b>

where solo.ckpool.org is the pool address, 3333 is the port number, next is your login name, which is often your BTC address, followed by your password, then the worker name (if the pool does not support worker names enter X) and finally a y or n to indicate if the pool supports custom difficulty settings.
The last configuration is for the asic chips. The easiest way to set these to a 'working' value is by entering

<b>save asic</b>

which will save the (safe and slow) asic settings as used during bootup of the miner. If you remember previously used settings you can write those to the asic configuration instead with

<b>write /asic.cfg:300 1350</b>

Where the first number is the frequency in MHz and the second is the core voltage in millivolt. 
You can tune these settings later using f+/f- & v+/v- commands. Now its time for (another) reboot so the miner will try to startup with the new configuration. Enter

<b>r</b>

and the miner will reboot. If the miner will not start mining you can check your configuration files by entering

<b>type filename</b>

where filename is one of the configuration files (don't forget the preceeding '/'). The miner will also report a missing (or very wrong) configuration file when booting but you will have to open its web page very soon after power up/reboot or you will miss it.

The miner will load the configuration files at each reboot so luckily you only have to do all of this once.

Tip: write all configuration commands in a text file on your pc or phone so you can copy & paste them instead of typing them when you want to (re)configure the miner. 
