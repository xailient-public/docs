# Reference Implementations - Sample Codes

## Detection on Static Image

``` python
from xailient import dnn
import cv2 as cv

#By default Low resolution DNN for face detector will be loaded.
#To load the high resolution Face detector please comment the below lines.

detectum = dnn.Detector()
THRESHOLD = 0.4 # Value between 0 and 1 for confidence score

im = cv.imread('../data/beatles.jpg')

_, bboxes = detectum.process_frame(im, THRESHOLD)

# Loop through list (if empty this will be skipped) and overlay green bboxes
# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
for i in bboxes:
    cv.rectangle(im, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)
    
cv.imwrite('../data/beatles_output.jpg', im)
```

## Detection on Video

``` python
import cv2 as cv
from xailient import dnn
import numpy as np

THRESHOLD = 0.4 # Value between 0 and 1 for confidence score

detectum = dnn.Detector()
cap = cv.VideoCapture("sample.mp4")

while True:
    _, next_frame = cap.read() # Reads the next video frame into memory
    _, bboxes = detectum.process_frame(next_frame, THRESHOLD) # Extract bbox coords

    # Loop through list (if empty this will be skipped) and overlay green bboxes
    # Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
    for i in bboxes:
        cv.rectangle(next_frame, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)

    cv.imshow("Rendered Video", next_frame)

    key = cv.waitKey(50)
    if key == 27: # Hit ESC key to stop
        break

cap.release()
cv.destroyAllWindows()
```

## Detection on Pi Camera Streaming Video

``` python

# This script has been tested using a Raspberry Pi Camera Modeule v1.3

from picamera.array import PiRGBArray
from picamera import PiCamera
import time
import cv2 as cv
import math
from xailient import dnn
import numpy as np

#By default Low resolution DNN for face detector will be loaded.
#To load the high resolution Face detector please comment the below lines.
detectum = dnn.Detector()

THRESHOLD = 0.45 # Value between 0 and 1 for confidence score

# initialize the camera and grab a reference to the raw camera capture
RES_W = 640 # 1280 # 640 # 256 # 320 # 480 # pixels
RES_H = 480 # 720 # 480 # 144 # 240 # 360 # pixels

camera = PiCamera()
camera.resolution = (RES_W, RES_H)
camera.framerate = 30 # FPS
rawCapture = PiRGBArray(camera, size=(RES_W, RES_H))

# allow the camera to warmup
time.sleep(0.1)

# capture frames from the camera
for frame in camera.capture_continuous(rawCapture, format="bgr", use_video_port=True):
    # grab the raw NumPy array representing the image, then initialize the timestamp
    # and occupied/unoccupied text
    image = frame.array
    image_cpy = np.copy(image) # Create copy since cant modify orig

    # Return's list of bounding box co-ordinates
    _, bboxes = detectum.process_frame(image, THRESHOLD)

    # Loop through list (if empty this will be skipped) and overlay green bboxes
    for i in bboxes:
        cv.rectangle(image_cpy, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)

    # show the frame
    cv.imshow("Frame", image_cpy)
    key = cv.waitKey(1) & 0xFF

    # clear the stream in preparation for the next frame
    rawCapture.truncate(0)

    # if the `q` key was pressed, break from the loop
    if key == ord("q"):
        break

```

## Send Detection Event to API using HTTP Post

``` python
# Import required libraries
from picamera.array import PiRGBArray
from picamera import PiCamera
from xailient import dnn
import cv2 as cv
import requests
import base64
import os
import json
import numpy as np

#By default Low resolution DNN for face detector will be loaded.
#To load the high resolution Face detector please comment the below lines.
detectum = dnn.Detector()

THRESHOLD = 0.45 # Value between 0 and 1 for confidence score

# api-endpoint
API_ENDPOINT = "<ENTER YOUR API ENDPOINT HERE>"
API_KEY = "<ENTER YOUR API KEY HERE, IF THERE IS NO API KEY, LEAVE THIS EMPY>"

def send_results(frame, bboxes):
    """
    This function is to send results to a web API using HTTP post.
    Parameters:
    
    frame: image as numpy array
    bboxes: list of list
    """

    # prepare headers for http request
    content_type = "application/json"
    headers = {}
    headers["content-type"] = content_type

    if API_KEY != "":
        headers["x-api-key"] = API_KEY

    # encode image to base64 string
    base64_string_image = encode(frame)

    # data to be sent to api 
    data = {
        "message" : "Object detected",
        "image": base64_string_image,
        "bboxes": bboxes
    }

    # convert the data to be sent to json
    data_json = json.dumps(data)

    print("Data to send to API: {}".format(data_json))

    # sending post request and saving response as response object 
    r = requests.post(url = API_ENDPOINT, data = data_json, headers = headers) 

    print("Response: {}".format(r))
    print("Response body: {}".format(r.text))

    if r.status_code == 200:
        print("Data sent to API successfully!")
        return True
    else:
        print("Failed to send data to API!")
        return False

def encode(image):
    """
    Encode image as base64 string.
    """

    file_name = "temp.png"
    base64_message = ""
    
    cv.imwrite(file_name, image)

    with open(file_name, 'rb') as binary_file:
        binary_file_data = binary_file.read()
        base64_encoded_data = base64.b64encode(binary_file_data)
        base64_message = base64_encoded_data.decode('utf-8')
    
    if os.path.isfile(file_name):
        print("Delete temp file")
        os.remove(file_name)
    
    return base64_message

def main():
    im = cv.imread('../data/beatles.jpg')

    _, bboxes = detectum.process_frame(im, THRESHOLD)

    # Loop through list (if empty this will be skipped) and overlay green bboxes
    # Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
    for i in bboxes:
        cv.rectangle(im, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)
    
    # If any object detected, send result to API using HTTP post
    if len(bboxes) > 0:
        send_results(im, bboxes)

    cv.imwrite('../data/beatles_output.jpg', im)

main()
```

## Post-processing Script to Improve Accuracy

``` python
#!/usr/bin/python3

from xailient import dnn
import cv2 as cv

#By default Low resolution DNN for face detector will be loaded.
#To load the high resolution Face detector please comment the below lines.
def main():
	detectum = dnn.Detector()
	THRESHOLD = 0.4 # Value between 0 and 1 for confidence score

	im = cv.imread('../data/beatles.jpg')

	_, bboxes = detectum.process_frame(im, THRESHOLD)


	# --- uncomment to utilise post-processing --- #
	# 1.
	# Post-processing to remove any bboxes whose coordinates are inside larger bboxes.
	# bboxes = remove_inside_bboxes(bboxes) # uncomment me!!!
	# 2.
	# Post-processing that combines any two overlapping bboxes into one larger bbox.
	# bboxes = combine_bboxes(bboxes) # uncomment me!!!


	# Loop through list (if empty this will be skipped) and overlay green bboxes
	# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
	for i in bboxes:
		cv.rectangle(im, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)

	cv.imwrite('../data/beatles_output.jpg', im)


#######################
### POST-PROCESSING ###
#######################

# 1. Post-processing to remove any bboxes whose coordinates are inside larger bboxes.
def remove_inside_bboxes(bboxes):
	filtered_bboxes = []
	for test_bbox in bboxes:
		if not smaller_bbox(test_bbox, bboxes):
			filtered_bboxes.append(test_bbox)
	return filtered_bboxes

def smaller_bbox(test_bbox, bboxes):
	t_xmin = test_bbox[0]
	t_ymin = test_bbox[1]
	t_xmax = test_bbox[2]
	t_ymax = test_bbox[3]

	for bbox in bboxes:
		if list(test_bbox) == list(bbox):
			continue

		b_xmin = bbox[0]
		b_ymin = bbox[1]
		b_xmax = bbox[2]
		b_ymax = bbox[3]

		# Return True if test_bbox coordinates is inside another bounding box
		if b_xmin <= t_xmin <= b_xmax and b_xmin <= t_xmax <= b_xmax \
		and b_ymin <= t_ymin <= b_ymax and b_ymin <= t_ymax <= b_ymax:
			return True
	return False


# 2. Post-processing that combines any two overlapping bboxes into one larger bbox.
def combine_bboxes(bboxes):
	not_matched_bboxes = []
	combined = []
	loop_again = True
	match = False

	while(loop_again):
		loop_again = False

		for bboxA in bboxes:
			for bboxB in bboxes:

				if bboxA != bboxB: # ignore the same bbox
					# determine the (x, y)-coordinates of the intersection rectangle
					xmin = max(bboxA[0], bboxB[0])
					ymin = max(bboxA[1], bboxB[1])
					xmax = min(bboxA[2], bboxB[2])
					ymax = min(bboxA[3], bboxB[3])

					# compute the area of intersection rectangle
					interArea = max(0, xmax - xmin) * max(0, ymax - ymin)

					# If intersection > 0, compute coordinates of combined bbox
					if interArea > 0:
						xmin = min(bboxA[0], bboxB[0])
						ymin = min(bboxA[1], bboxB[1])
						xmax = max(bboxA[2], bboxB[2])
						ymax = max(bboxA[3], bboxB[3])

						if [xmin,ymin,xmax,ymax] not in combined:
							combined.append([xmin,ymin,xmax,ymax])

						match = True
						loop_again = True # We need to loop again to ensure this combined bbox
								  # is not overlapping with another bbox

			if match == False: # if bboxA doesn't overlap with any other bbox in this current interation
				if bboxA not in not_matched_bboxes:
					not_matched_bboxes.append(bboxA)
			match = False

		bboxes = combined.copy()
		bboxes.extend(not_matched_bboxes)
		combined = []

	return bboxes



if __name__ == "__main__":
	main()
```