!pip install easyocr

import easyocr
import cv2
from matplotlib import pyplot as plt
import numpy as np

IMAGE_PATH = '/content/human.jpeg'

reader = easyocr.Reader(['en'])
result = reader.readtext(IMAGE_PATH)
result

top_left = tuple(result[0][0][0])
bottom_right = tuple(result[0][0][2])
text = result[0][1]
font = cv2.FONT_HERSHEY_SIMPLEX

img = cv2.imread(IMAGE_PATH)
img = cv2.rectangle(img,top_left,bottom_right,(0,255,0),3)
img = cv2.putText(img,text,top_left, font, 0.5,(255,255,255),2,cv2.LINE_AA)
plt.imshow(img)
plt.show()

img = cv2.imread(IMAGE_PATH)
spacer = 100
for detection in result: 
    top_left = tuple(int(val) for val in detection[0][0]) # convert values to integers
    bottom_right = tuple(int(val) for val in detection[0][2]) # convert values to integers
    text = detection[1]
    img = cv2.rectangle(img,top_left,bottom_right,(0,255,0),3)
    img = cv2.putText(img,text,(20,spacer), font, 0.5,(0,255,0),2,cv2.LINE_AA)
    spacer+=15
    
plt.imshow(img)
plt.show()
