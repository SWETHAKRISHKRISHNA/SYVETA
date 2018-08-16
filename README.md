# SYVETA
/*importing packages for image detection*/
from imageai.Detection import ObjectDetection
import os

/*importing packages for videocapture*/
import numpy as np
import cv2

/*importing packages for sound detection*/
from time import sleep
import RPi.GPIO as GPIO

/*importing packages for holograph clone */
import webbrowser

/*code to capture scenes in traffic*/
cap = cv2.VideoCapture('videos/wa.avi')
while(cap.isOpened()):
  ret, frame = cap.read()
  gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
  cv2.imshow('frame',gray)
  if cv2.waitKey(1) & 0xFF == ord('q'):
    break

cap.release()
cv2.destroyAllWindows()

/*code to detect ambulance by object recognition*/
execution_path = os.getcwd()

detector = ObjectDetection()
detector.setModelTypeAsRetinaNet()
detector.setModelPath(os.path.join(execution_path,"resnet50_coco_best_v2.0.1.h5"))
detector.loadModel()
detections= detector.detectObjectsFromImage(input_image=os.path.join(execution_path, "image.jpg"), output_image_path=os.path.join(execution_path, "imagenew.jpg"))

for eachObject in detections:
    print(eachObject["name"] , " : " , eachObject["percentage_probability"] )
view raw

/*fetch the ambulance object alone to check the condition*/

/*code to detect sound */
/*record the ambulance siren sound in audio file to compare with the sound detected by sound detection sensor */
    GPIO.setmode(GPIO.BCM)
    # define input pin
    pin = 12
    GPIO.setup(pin, GPIO.IN)

    try:
	    while True:
		    if GPIO.input(pin) == GPIO.LOW:
		    	    print("no sound", "/", GPIO.input(pin))	
		    else:
			    print("siren sound is matched", "/", GPIO.input(pin))
			    sleep(0.1)
		    sleep(0.1)	
    finally:
        GPIO.cleanup()

/*check the condition*/
/*use if statement to check both the detection process of sound and object(ambulance)*/
/*if the condition is true ,the holographic clone is generated*/


/*code to holographic clone*/
/*3D holographic clone is recorded in a video file to tell the pedestrians that "DEAR CITIZENS,THE AMBULANCE IS ON THE WAY,GIVE THEM WAY TO PASS THE SIGNAL"*/
/*The video is stored in ppt and is embedded in holo.html file as to use simple code*/

f = open('holo.html','r')
//use view commands to display video file
f.close()


/*another way to generate the holographic clone is by python programming using hologram packages*/



/*continue the capturing process for the next ambulance detection */
