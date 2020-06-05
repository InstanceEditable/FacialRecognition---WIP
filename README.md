# ImageAnalysis
import cv2
import numpy as np
import matplotlib as plt


#imagePath = 'filepath/ABBA.jpg'
cascPath = 'filepath/haarcascade_frontalface_default.xml'
# Create the haar cascade
faceCascade = cv2.CascadeClassifier(cascPath)
# Read the image
image = cv2.imread(imagePath)
image = np.array(image, dtype=np.uint8)
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
# Detect faces in the image
faces = faceCascade.detectMultiScale(
    gray,
    scaleFactor=1.2,
    minNeighbors=5,
    minSize=(30, 30),
    flags = cv2.CASCADE_SCALE_IMAGE)

# Draw a rectangle around the faces
for (x, y, w, h) in faces:
    cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2)


cv2.imshow("Faces found", image)
cv2.waitKey(0)
