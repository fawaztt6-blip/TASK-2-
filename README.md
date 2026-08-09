# Color Recognition Using OpenCV
import cv2
import numpy as np

colors = {
"Red": [
(np.array([0, 120, 70]), np.array([10, 255, 255])),
(np.array([170, 120, 70]), np.array([179, 255, 255]))
],
"Green": [
(np.array([35, 70, 50]), np.array([85, 255, 255]))
],
"Blue": [
(np.array([90, 80, 50]), np.array([130, 255, 255]))
],
"Yellow": [
(np.array([20, 100, 100]), np.array([35, 255, 255]))
]
}

selected_color = "Red"

camera = cv2.VideoCapture(0)

while True:

success, frame = camera.read()

if not success:
break

frame = cv2.flip(frame, 1)

hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

mask = np.zeros(hsv.shape[:2], dtype=np.uint8)

for lower, upper in colors[selected_color]:
mask = mask | cv2.inRange(hsv, lower, upper)

kernel = np.ones((5, 5), np.uint8)

mask = cv2.morphologyEx(
mask,
cv2.MORPH_OPEN,
kernel
)

mask = cv2.morphologyEx(
mask,
cv2.MORPH_CLOSE,
kernel
)

contours, _ = cv2.findContours(
mask,
cv2.RETR_EXTERNAL,
cv2.CHAIN_APPROX_SIMPLE
)

if contours:

largest = max(contours, key=cv2.contourArea)

if cv2.contourArea(largest) > 800:

x, y, w, h = cv2.boundingRect(largest)

cv2.rectangle(
frame,
(x, y),
(x + w, y + h),
(255, 255, 255),
2
)

cv2.putText(
frame,
selected_color + " detected",
(x, y - 10),
cv2.FONT_HERSHEY_SIMPLEX,
0.8,
(255, 255, 255),
2
)

cv2.putText(
frame,
"Color: " + selected_color,
(20, 35),
cv2.FONT_HERSHEY_SIMPLEX,
0.8,
(255, 255, 255),
2
)

cv2.imshow("Color Recognition", frame)

key = cv2.waitKey(1) & 0xFF

if key == ord("r"):
selected_color = "Red"

elif key == ord("g"):
selected_color = "Green"

elif key == ord("b"):
selected_color = "Blue"

elif key == ord("y"):
selected_color = "Yellow"

elif key == ord("q"):
break

camera.release()
cv2.destroyAllWindows()




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


HuskyLens Color Recognition

`HuskyLens_Color_Recognition.ino`

```cpp
#include <Wire.h>
#include "HUSKYLENS.h"

HUSKYLENS huskylens;

void setup()
{
Serial.begin(115200);

Wire.begin();

while (!huskylens.begin(Wire))
{
Serial.println("HuskyLens connection failed");
delay(1000);
}

Serial.println("HuskyLens connected");

while (!huskylens.writeAlgorithm(ALGORITHM_COLOR_RECOGNITION))
{
Serial.println("Color Recognition failed");
delay(500);
}

Serial.println("Color Recognition started");
}

void loop()
{
if (!huskylens.request())
{
Serial.println("Request failed");
delay(500);
return;
}

if (huskylens.available())
{
HUSKYLENSResult result = huskylens.read();

Serial.print("Color ID: ");
Serial.println(result.ID);

Serial.print("X: ");
Serial.println(result.xCenter);

Serial.print("Y: ");
Serial.println(result.yCenter);

Serial.print("Width: ");
Serial.println(result.width);

Serial.print("Height: ");
Serial.println(result.height);

Serial.println("Color detected");
Serial.println("----------------");
}
else
{
Serial.println("No color detected");
}

delay(500);
}


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
