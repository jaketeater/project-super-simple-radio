# Overview #

## Connecting to the radio for programming and debugging ##
There are two ways to connect: 

1. USB->Serial, using pads on the PCB
2. On board USB, via micro USB port on the PCB

USB->Serial appears to be the best for troubleshooting and development, as it is more verbose. To save money, this is achieved by connecting an extermal USB->Serial cable to pads on the PCB. This way one set of USB->Serial hardware can be used for multiple devices.

The ESP32 S3's onboard OTG USB does not appear to recieve the ESP32's debug messages, so it's not a solution for troubleshooting and development. However, it does provide a cheap way to make firmware updates more convenient.

### Linux ###

Create a udev rule so that it is not necessary to set permissions with each connection, by creating this file `/etc/udev/rules.d/99-esp32s3.rules` and adding this line:

`ATTRS{idVendor}=="303a", ATTRS{idProduct}=="1001", MODE="0666", ENV{ID_MM_DEVICE_IGNORE}="1", ENV{ID_MM_PORT_IGNORE}="1"`

Then restart udev:

`sudo systemctl restart udev`

# Version Name #

v<version>-<antenna type><audio output><station select><configuration location>

- version: version number - corresponds with firmware
- antennta type: 
    O) onboard ESP32 antenna
    P) external antenna
- audio output:
    S) speakers
    L) line out
- station select:
    S) single station (no selector)
    M) multi station
- configuration location
    H) hardcoded
    R) remote

# Useful Resources #
- Espressif ESP32 hardware design guidelines https://www.espressif.com/sites/default/files/documentation/esp32_hardware_design_guidelines_en.pdf
- Schematics for the ESP32 S3 dev board https://dl.espressif.com/dl/schematics/SCH_ESP32-S3-DevKitC-1_V1.1_20220413.pdf
- Arduino-ESP32 Documentation https://docs.espressif.com/projects/arduino-esp32/en/latest/getting_started.html 