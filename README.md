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
 # pip install opencv-python numpy
