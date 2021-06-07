# Running Multiple Xailient Models on a Single Device

If you need to run more that one Xailient model on a single device, please follow this tutorial.

For this tutorial, we will use two models, pre-trained Car Detector and a pre-trained License Plate Detector.

## Device Setup

To meet the minimum requirements, your device must be a x86_64 or ARM32 architecture device. We've tested the following operating systems:

* Ubuntu 18.04 LTS
* Ubuntu 19.04
* Raspbian Buster

!!! note

    To run Xailient SDK on Windows or MacOS, please run it inside a VirtualBox.

    Here are some resources you can refer to to install Ubuntu operating system on a VirtualBox:

    * [Resource 1](https://brb.nci.nih.gov/seqtools/installUbuntu.html)
    * [Resource 2](https://medium.com/@tushar0618/install-ubuntu-16-04-lts-on-virtual-box-desktop-version-30dc6f1958d0)
    * [Resource 3](https://itsfoss.com/install-linux-in-virtualbox/)


For ARM32, we have tested on the following device:

* RaspberryPi 3B+

__Minimum software requirements:__

* Glibc 2.27
* Python3.7
* Pip for python3.7
* OpenCV
* Curl
* VirtualEnv

If your device does not meet the minimum software required, please follow the instructions below to install them.

__Download the package lists and update information__

```bash
$ sudo apt-get update
```

!!! note
    apt-get update to download the package lists from the repositories and "update" them to get information on the newest versions of packages and their dependencies. It will do this for all repositories and PPAs.

__Install python3.7__

```bash
$ sudo apt-get install python3.7
```

__Install pip for python3.7__

```bash
$ sudo apt-get install python3-pip
```

__Install OpenCV__

```bash
$ sudo apt-get install python-opencv
```

__Install Curl__

```bash
$ sudo apt-get install curl
```

__Install VirtualEnv__

```bash
$ python3.7 -m pip install --user virtualenv
```

## Install Multiple Models

Create a separate virtual environment for each model you want to install.

For this tutorial, we will create two virtual environments, one to install the Car Detector and another to install License Plate Detector.

### Car Detector

__Create a Virtual Environment for Car Detector__

Create a new python virtual environment to isolate package installation for the system.

```bash
$ python3.7 -m venv car_detector_env
```

Activate the virtual environment.

Before you can start using the virtual environment for package installations, you will need to activate it. Activating a virtual environment will put the virtual environment-specific python and pip executables into your shell's PATH.

```bash
$ source car_detector_env/bin/activate
```

__Install Car Detector SDK__

!!! note
    In 18.04 Ubuntu, by default __pip3__ is for python3.6. So we will use __python3.7 -m pip__ command instead to use pip for python3.7.
    If pip3 for your device defaults to python3.7, feel free to replace the command __python3.7 -m pip__ with __pip3__.

__Get SDK Wheel Link__

Go to the Console and navigate to __MANAGE AI MODELS__. For the model you want to deploy, select the SDK you have build for your target platform. 

!!! note
    If you have not build an SDK yet, refer to __Build SDK__ section of the documentation.

Click on the target platform for the model to download and copy the SDK link.

<p align="center">
  <img src="../latest/img/console/CopySDKLink_CarDetector.png">
</p>

!!! note
    When you click the button &lt;ARM32&gt; or &lt;x86_64&gt;, it downloads the SDK wheel file as well as copies the link to the wheel file in your clipboard.

__Install SDK Wheel__

#### Install using downloaded SDK wheel file

```bash
(car_detector_env) $ python3.7 -m pip install <download_path/wheel_file_name>
```

##### Install using SDK link

```bash
(car_detector_env) $ python3.7 -m pip install "<SDK WHEEL LINKs>"
```

!!! note
    Replace &lt;SDK WHEEL LINK&gt; with the SDK link you copied earlier from the console.

__Info about xailient sdk installed__

```bash
(car_detector_env) $ python3.7 -m pip show xailient
```

You can get information about the version of xailient sdk installed, support email address, and location of the installation. 

!!! note
    Keep note of the install location "Location" as you will need it in the steps below.

__Go to Xailient Installation Folder__

To go to xailient folder, use the following command. If you do not know the install location, please refer to __"Info about xailient sdk installed"__ section above.

```bash
(car_detector_env) $ cd <Xailient Install Location>/xailient
```

__Xailient SDK contents__

```bash
(car_detector_env) $ ls
```

* bin/ -- Executables required for initial registration
* data/ -- Image files you can use with the sample applications
* samples/ -- Sample application demonstrating how the Xailient SDK library can be used
* scripts/ -- License activation scripts
* sharedLib_x86_64/ --Sample models that can be installed or linked with your applications


__Install tflite runtime__

Install the tflite runtime using requirements.txt file.

```bash
(car_detector_env) $ python3.7 -m pip install -r requirements.txt
```

__Install flask__

```bash
(car_detector_env) $ python3.7 -m pip install flask
```

__Activate your license__

Go to __scripts__ folder and execute xailient-install script

```bash
(car_detector_env) $ cd scripts
(car_detector_env) $ sudo ./xailient-install
```

__Deactivate virtual environment__

To deactivate the virtual environment,

```bash
(car_detector_env) $ deactivate
```

### License Plate Detector

__Create a Virtual Environment for License Plate Detector__

Now, create a new python virtual environment for License Plate Detector

```bash
$ python3.7 -m venv license_plate_detector_env
```

Activate the virtual environment.

Before you can start using the virtual environment for package installations, you will need to activate it. Activating a virtual environment will put the virtual environment-specific python and pip executables into your shell's PATH.

```bash
$ source license_plate_detector_env/bin/activate
```

__Install License Plate Detector SDK__

Download the SDK or get the SDK link from Xailient AI Console.

Go to the Console and navigate to __MANAGE AI MODELS__. For the model you want to deploy, select the SDK you have build for your target platform. 

!!! note
    If you have not build an SDK yet, refer to __Build SDK__ section of the documentation.

Click on the target platform for the model to download and copy the SDK link.

<p align="center">
  <img src="../latest/img/console/CopySDKLink_LicensePlateDetector.png">
</p>

!!! note
    When you click the button &lt;ARM32&gt; or &lt;x86_64&gt;, it downloads the SDK wheel file as well as copies the link to the wheel file in your clipboard.

__Install SDK Wheel__

##### Install using downloaded SDK wheel file

```bash
(license_plate_detector_env) $ python3.7 -m pip install <download_path/wheel_file_name>
```

##### Install using SDK link

```bash
(license_plate_detector_env) $ python3.7 -m pip install "<SDK WHEEL LINKs>"
```

!!! note
    Replace &lt;SDK WHEEL LINK&gt; with the SDK link you copied earlier from the console.

__Info about xailient sdk installed__

```bash
(license_plate_detector_env) $ python3.7 -m pip show xailient
```

You can get information about the version of xailient sdk installed, support email address, and location of the installation. 

!!! note
    Keep note of the install location "Location" as you will need it in the steps below.

__Go to Xailient Installation Folder__

To go to xailient folder, use the following command. If you do not know the install location, please refer to __"Info about xailient sdk installed"__ section above.

```bash
(license_plate_detector_env) $ cd <Xailient Install Location>/xailient
```

__Xailient SDK contents__

```bash
(license_plate_detector_env) $ ls
```

* bin/ -- Executables required for initial registration
* data/ -- Image files you can use with the sample applications
* samples/ -- Sample application demonstrating how the Xailient SDK library can be used
* scripts/ -- License activation scripts
* sharedLib_x86_64/ --Sample models that can be installed or linked with your applications


__Install tflite runtime__

Install the tflite runtime using requirements.txt file.

```bash
(license_plate_detector_env) $ python3.7 -m pip install -r requirements.txt
```

__Install flask__

```bash
(license_plate_detector_env) $ python3.7 -m pip install flask
```

__Activate your license__

Since you have already activated your license for this device earlier, YOU DO NOT NEED TO REPEAT THIS STEP.

__Deactivate virtual environment__

To deactivate the virtual environment,

```bash
(license_plate_detector_env) $ deactivate
```

## Setup Flask Server

Now, we will setup two flask servers, one for Car Detector and another for License Plate Detector, so we can access both models using REST API.

!!! note
    Make sure to use different ports for different flask servers.


### Flask server code for Car Detector

*file_name: flask_server_car_detector.py*

``` python
from xailient import dnn
from flask import Flask, jsonify, request
import cv2
import numpy
import time
import json

app = Flask(__name__)
detectum = dnn.Detector()

@app.route('/process', methods=['POST'])
def process_frame():
	start_time = time.time()
	data = request.files['file']
	im = cv2.imdecode(numpy.fromstring(request.files['file'].read(), numpy.uint8), cv2.IMREAD_UNCHANGED)
	THRESHOLD = 0.4 # Value between 0 and 1 for confidence score
	inference_start_time = time.time()
	
	
	_, bboxes = detectum.process_frame(im, THRESHOLD)
	inference_end_time = time.time()

	# Loop through list (if empty this will be skipped) and overlay green bboxes
	# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
	response = {}
	boxes = []
	for i in bboxes:
		bbox = {}
		bbox["xmin"] = int(i[0])
		bbox["ymin"] = int(i[1])
		bbox["xmax"] = int(i[2])
		bbox["ymax"] = int(i[3])
		boxes.append(bbox)
		cv2.rectangle(im, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)
	
	response["bboxes"] = boxes
	response["class"] = "car"
	cv2.imwrite("output.jpg", im)   

	print(response)

	#return "hello"
	return jsonify(response)

app.run("0.0.0.0", port=8001)
```

### Flask server code for License Plate Detector

*file_name: flask_server_license_plate_detector.py*

``` python
from xailient import dnn
from flask import Flask, jsonify, request
import cv2
import numpy
import time
import json

app = Flask(__name__)
detectum = dnn.Detector()

@app.route('/process', methods=['POST'])
def process_frame():
	start_time = time.time()
	data = request.files['file']
	im = cv2.imdecode(numpy.fromstring(request.files['file'].read(), numpy.uint8), cv2.IMREAD_UNCHANGED)
	THRESHOLD = 0.4 # Value between 0 and 1 for confidence score
	inference_start_time = time.time()
	
	
	_, bboxes = detectum.process_frame(im, THRESHOLD)
	inference_end_time = time.time()

	# Loop through list (if empty this will be skipped) and overlay green bboxes
	# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
	response = {}
	boxes = []
	for i in bboxes:
		bbox = {}
		bbox["xmin"] = int(i[0])
		bbox["ymin"] = int(i[1])
		bbox["xmax"] = int(i[2])
		bbox["ymax"] = int(i[3])
		boxes.append(bbox)
		cv2.rectangle(im, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)
	
	response["bboxes"] = boxes
	response["class"] = "plate"
	cv2.imwrite("output.jpg", im)   

	print(response)

	#return "hello"
	return jsonify(response)

app.run("0.0.0.0", port=8002)
```

## Start Flask Servers on different virtual environments

Since our Car Detector is insalled in one virtual environment and License Plate is installed in another, we need to run the above flask servers on their respective virtual environments.

Here is a bash script to do that:

*file_name: start.sh*

``` bash
#!/bin/sh
chmod +x flask_server_car_detector.py
chmod +x flask_server_license_plate_detector.py

/<path-to-virtual-env>/car_detector_env/bin/python3.7 flask_server_car_detector.py &
/<path-to-virtual-env>/license_plate_detector_env/bin/python3.7 flask_server_license_plate_detector.py 
```

Now run the bash script to start these servers:

``` bash
sudo ./start.sh
```

## Write a python script to send images to these detectors using REST API and get back inference.

``` python
# install request using pip3 install requests
import requests
import json

def run_car_detector(image_path):
    url = 'http://127.0.0.1:8001/process'
    files = {'file': open(image_path, 'rb')}
    response = requests.post(url, files=files)

    res_json =  json.loads(response.text)
    print(res_json)
    return res_json

def run_licen_pate_detector(image_path):
    url = 'http://127.0.0.1:8002/process'
    files = {'file': open(image_path, 'rb')}
    response = requests.post(url, files=files)

    res_json =  json.loads(response.text)
    print(res_json)
    return res_json
```

