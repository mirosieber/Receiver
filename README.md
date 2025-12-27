# Modified to be non-blocking to keep loop fast.
This library has been forked and modified to use an interrupt pin for measuring the signals from an RC receiver. This results in fast non-blocking main loop execution.

## Works only on ESP32 boards!


# ESP32 Receiver Library

ESP32 library for reading RC receiver values using interrupts

## Installing the Library
### From repo
Click the code button.
Then download as zip.
Then in the Arduino IDE, install the zip library.
See the [Arduino official guide](https://www.arduino.cc/en/guide/libraries).

## How to use
### Import the library 
```c++
#include <RC_Receiver.h>
```

### Initialize the receiver
```c++
RC_Receiver receiver;
```

### Set the pins for each channel
```c++
std::vector<uint8_t> pins = {7, 8, 4, 5};
```

### Set custom min and max values for the mapping of each channel
Set custom values for the range of the controller.
The values can be found by using the RC_raw example and moving the joystick to its min and max positions and reading the values.
Inverting the min and max will reverse the values.
```c++
std::vector<std::pair<uint16_t, uint16_t>> minMax = 
{
	{544,2400}, 
	{544,2400}, 
	{544,2400}, 
	{544,2400} 
};

void setup() {
	receiver.init(pins, minMax);
}

```

### Get raw values
getRaw(int ch) will return the raw value from the controller.
The `ch` is the channel number.
```c++
Serial.print(receiver.getRaw(int ch));
```

### Get mapped values
getMap(int ch) will return the mapped value (0 to 1000) from the controller.
The `ch` is the channel number.
```c++
Serial.print(receiver.getMap(int ch));
```