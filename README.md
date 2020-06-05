# Traffic Detection

import cv2
import sys
import numpy as np

#open the camera
video_capture= cv2.VideoCapture(0)

#get cascade classifiers
peopleCascade= cv2.CascadeClassifier('haarcascade_fullbody.xml')
signCascade= cv2.CascadeClassifier('TrafficLight_HAAR_16Stages.xml')
carCascade= cv2.CascadeClassifier('cars.xml')

while True:
    # Capture frame-by-frame
    ret, frame = video_capture.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    stopLights = signCascade.detectMultiScale(
        gray,
        scaleFactor=1.1,
        minNeighbors=5,
        minSize=(30, 30),
        flags=cv2.CASCADE_SCALE_IMAGE
    )

    # Draw a rectangle around the faces
    for (x, y, w, h) in stopLights:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 0, 255), 2)

    cars = carCascade.detectMultiScale(
        gray,
        scaleFactor=1.5,
        minNeighbors=5,
        minSize=(30, 30),
        flags=cv2.CASCADE_SCALE_IMAGE
    )

    # Draw a rectangle around the cars
    for (x, y, w, h) in cars:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)

    # Display the resulting frame
    cv2.imshow('Video', frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

#release the capture
video_capture.release()
cv2.destroyAllWindows()
