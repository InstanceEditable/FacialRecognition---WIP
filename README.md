# ImageAnalysis
import numpy as np
import cv2
from time import sleep


#Open the camera
cv2.namedWindow("preview")
vidcap = cv2.VideoCapture(0)
#success,image = vidcap.read()

while True:
    #If the camera is not available
    if not vidcap.isOpened():
        print('Unable to load camera.')
        sleep(5)
        pass

if vidcap.isOpened(): # try to get the first frame
    rval, frame = vc.read()
else:
    rval = False

while rval:
    #Create a window to view camera
    cv2.imshow("preview", frame)
    rval, frame = vc.read()
    key = cv2.waitKey(20)
    if key == 27: # exit on ESC
        break

vidcap.release()
cv2.destroyAllWindow("preview")
