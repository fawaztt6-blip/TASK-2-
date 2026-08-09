# Color Recognition Using OpenCV

## Description

This project uses Python and OpenCV to recognize colors in real time using a webcam.

The program can recognize:

- Red
- Green
- Blue
- Yellow

When the selected color is detected, the program draws a rectangle around the object.

## Requirements

- Python
- OpenCV
- NumPy
- Webcam

## Installation

Install the required libraries:

```bash
pip install opencv-python numpy

_____________________________________________________________________________________________________________________________________

# Color Recognition Using HuskyLens

## Description

This project uses HuskyLens and Arduino Uno to recognize colors.

HuskyLens detects the color and sends the detection information to Arduino using I2C communication.

Arduino displays the detected information in the Serial Monitor.

## Requirements

- HuskyLens
- Arduino Uno
- USB cable
- HuskyLens cable
- Arduino IDE

## Connection

HuskyLens VCC → Arduino 5V

HuskyLens GND → Arduino GND

HuskyLens SDA → Arduino A4

HuskyLens SCL → Arduino A5

## Setup

Set HuskyLens to:

Color Recognition

Set the communication protocol to:

I2C

## Installation

Install the HUSKYLENS Arduino library.

Open the Arduino IDE and upload:

HuskyLens_Color_Recognition.ino

## Run

After uploading the program, open the Serial Monitor.

Set the baud rate to:

115200

Place a colored object in front of HuskyLens.

## Result

HuskyLens recognizes the color and sends the detection information to Arduino.

The Serial Monitor displays:

- Color ID
- X position
- Y position
- Width
- Height

## How It Works

HuskyLens captures the image using its camera.

The Color Recognition algorithm detects the color.

The detected information is sent to Arduino through I2C.

Arduino reads the information and displays it through the Serial Monitor.

## Conclusion

This project demonstrates real-time color recognition using HuskyLens and Arduino Uno.
