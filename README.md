# aSiNine-ESP-miner (WIP)
Bitcoin miner for BM1387/BM1397 asics on an ESP microcontroller

# (WIP'ing now) Documents first, starting with the built instructions
To compile this software you need

- Arduino IDE (version 1.8.19 or above)
- Support for Espressif ESP's
- Library: PT8211 (see my repositories, extract to your library folder), needed for measuring Vcore with a PT8211s
- Library: WebSerialLite_S9 (see my repositories, extract to your library folder)
- Library: Freenove_WS2812_Lib_for_ESP32 (add with library manager in IDE), needed for the RGB led
- Library: ESPAsyncWebServer (add with library manager in IDE)
- Library: AsyncElegantOTA (add with library manager in IDE)
- Library: ESP32AnalogRead (add with library manager in IDE)
- The contents of this repository, download as zip and extract to your documents/arduino folder
