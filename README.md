**Note: This repository is deprecated. Please use our new drivers:**
* Uart: https://github.com/Sensirion/arduino-uart-sps30
* I2C: https://github.com/Sensirion/arduino-i2c-sps30

# Arduino library for the SPS30 particulate matter sensor

To learn more about the SPS30, please visit https://www.sensirion.com/sps30/.
For support questions on the SPS30, please visit https://sensirion.com/contact.

This library is using the code from Sensirion's
[embedded-sps](https://github.com/Sensirion/embedded-sps) library, and adding a
handful of changes to adapt to Arduino.

Most notably, for AVR based platforms (like Arduino Uno and friends), this is
using an alternative
[I2C Master Library](https://github.com/DSSCircuits/I2C-Master-Library) to work
around the I2C buffer size limit that exists on those boards.

## Compatibility

This library has been tested on the following platforms:
- AVR based Arduino, like Arduino Uno
- ESP8266, using v2.5.0 or newer (Tested on Adafruit Feather Huzzah ESP8266)
- ESP32, using v1.0.1 or newer (Tested on Adafruit Feather Huzzah ESP32)
- SAMD (tested on Arduino MKR 1010)

## Hardware setup

**Important Notes:** 

* The SPS30 requires 5V supply voltage +/-0.5V in order to provide correct
  output values; the SPS30 should be compatible with 3.3V I2C levels, so as 
  long as the supply voltage is correct the SPS30 should work fine with 3.3V 
  setups
* Make sure that the SPS30's Pin 4 ("Interface select") is connected to GND, on
  power-up of the sensor, otherwise the sensor works in UART instead of I2C
  mode and this driver will not detect the sensor. Note that the
  interface-select configuration is read on every start of the sensor including
  after a soft-reset.



### ESP8266 partial legacy support

This library automatically detects ESP8266 core versions 2.3.0, 2.4.0, 2.4.1 and
2.4.2 and supports a limited subset of functionality on there. The following
features are not available:
- Reading out number concentrations,
- Reading out the average particle size
- Reading out the serial number

## Installation

### Through the Arduino IDE

This library is available through Arduino IDE's Library Manager. To install,
select ```Tools```> ```Manage Libraries...```, then search for
```sensirion-sps```. Select the matching library and press ```Install```.

### Manual installation

For manual installation, follow these steps:

1. Download the latest ZIP file from the
   [Github release page](https://github.com/Sensirion/arduino-sps/releases/latest)
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
1. Open the serial plotter from the Tools menu (if you have the serial monitor
   open, you'll need to close it first)
1. Uncomment line 8 of the sample program; it should now read
   ```#define PLOTTER_FORMAT```
1. Press the "Upload" button to compile and upload the sketch

If you check the serial plotter window, you should see something like this:


![Serial monitor](doc/sps30-arduino-serial-plotter.jpg)


## FAQ: How PMx is defined / Why values are the same

A frequently asked question about values that are the same, which seems unlikely. However, this is due to the definition of PM_x_, that says that it's particles of diameter _x_ and smaller. As such, PM10 includes all particles of diameter 10 μm and smaller, and therefore includes particles from PM4 (which itself includes particles from PM2.5). To illustrate, here's a diagram that shows this 

![How PMx is defined](https://user-images.githubusercontent.com/1300460/121040377-b445d880-c766-11eb-82d9-241dcdefab1f.png)

In this example:
- PM2.5 would be 3.1 μg/m^3
- PM4 would be 3.2 μg/m^3 (3.1 particles [2.5 and smaller] + 0.1 [>2.5, <= 4.0])
- PM10 would be 3.2 μg/m^3 (3.1 particles [2.5 and smaller] + 0.1 [>2.5, <= 4.0] + 0 [>4.0 <= 10])
