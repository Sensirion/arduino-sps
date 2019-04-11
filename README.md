# Arduino library for the SPS30 particulate matter sensor

To learn more about the SPS30, please visit https://www.sensirion.com/sps30/. For support questions on the SPS30, please visit https://sensirion.com/contact.

This library is using the code from Sensirion's [embedded-sps](https://github.com/Sensirion/embedded-sps) library, and adding a handful of changes to adapt to Arduino.

Most notably, for AVR based platforms (like Arduino Uno and friends), this is using an alternative [I2C Master Library](https://github.com/DSSCircuits/I2C-Master-Library) to work around the I2C buffer size limit that exists on those boards.

## Compatibility

This library has been tested on the following platforms:
- AVR based Arduino, like Arduino Uno
- ESP8266, using v2.5.0 or newer (Tested on Adafruit Feather Huzzah ESP8266)
- ESP32, using v1.0.1 or newer (Tested on Adafruit Feather Huzzah ESP32)
- SAMD (tested on Arduino MKR 1010)

**Important Note:** The SPS30 requires 5V input voltage +/-0.5V in order to provide correct output values. When using a 3.3V based Arduino,
make sure to use the appropriate voltage regulators and level shifters for I2C!

## Installation

At this point, this library is not yet available through the Arduino Library manager. To install, following the following steps:

1. Download the latest ZIP file from the [Github release page](https://github.com/winkj/arduino-sps/releases/latest)
1. Start the Arduino IDE
1. Select ```Sketch > Include Library > Add .ZIP Library...```
1. A dialog will open; here, select the file you selected in step 1

## Usage

### Serial Monitor (Text output)

1. Open the example from ```File > Examples > arduino-sps > sps30```. 
1. Open the serial monitor from the Tools menu
1. Press the "Upload" button to compile and upload the sketch

If you check the serial monitor window, you should see something like this:

![Serial monitor](doc/sps30-arduino-serial-monitor.jpg)

### Serial Plotter (Graphical output)

1. Open the example from ```File > Examples > arduino-sps > sps30```. 
1. Open the serial plotter from the Tools menu (if you have the serial monitor open, you'll need to close it first)
1. Uncomment line 8 of the sample program; it should now read ```#define PLOTTER_FORMAT```
1. Press the "Upload" button to compile and upload the sketch

If you check the serial plotter window, you should see something like this:


![Serial monitor](doc/sps30-arduino-serial-plotter.jpg)
