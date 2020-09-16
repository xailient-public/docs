# Deploy Your AI

!!! note
      This version of the documentation is for installation of Xailient SDK using wheel file (.whl). 
      If you are looking for documentation for installion of Xailient SDK using SDK package, please visit our old [documentation](https://xailient.readthedocs.io/en/latest/installation/).
      
      If your local machines doesn't meet the requirements for native installation we also offer Docker [Containers as a deployment option](https://xailient-docs.readthedocs.io/en/latest/container/).

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

__Create a Virtual Environment (Recommended)__

Create a new python virtual environment to isolate package installation for the system.

```bash
$ python3 -m venv env
```

Activate the virtual environment.

Before you can start using the virtual environment for package installations, you will need to activate it. Activating a virtual environment will put the virtual environment-specific python and pip executables into your shell's PATH.

```bash
$ source env/bin/activate
```

To deactivate the virtual environment later,

```bash
(env) $ deactivate
```

## Install XailientSDK

!!! note
    In 18.04 Ubuntu, by default __pip3__ is for python3.6. So we will use __python3.7 -m pip__ command instead to use pip for python3.7.
    If pip3 for your device defaults to python3.7, feel free to replace the command __python3.7 -m pip__ with __pip3__.

__Get SDK Wheel Link__

Go to the Console and navigate to __MANAGE AI MODELS__. For the model you want to deploy, select the SDK you have build for your target platform. 

!!! note
    If you have not build an SDK yet, refer to __Build SDK__ section of the documentation.

Click on the target platform for the model to download and copy the SDK link.

<p align="center">
  <img src="../img/console/CopySDKLink.png">
</p>

!!! note
    When you click the button &lt;ARM32&gt; or &lt;x86_64&gt;, it downloads the SDK wheel file as well as copies the link to the wheel file in your clipboard.

__Install SDK Wheel__

##### Install using downloaded SDK wheel file

```bash
(env) $ python3.7 -m pip install <download_path/wheel_file_name>
```

##### Install using SDK link

```bash
(env) $ python3.7 -m pip install "<SDK WHEEL LINKs>"
```

!!! note
    Replace &lt;SDK WHEEL LINK&gt; with the SDK link you copied earlier from the console.

__Info about xailient sdk installed__

```bash
(env) $ python3.7 -m pip show xailient
```

You can get information about the version of xailient sdk installed, support email address, and location of the installation. 

!!! note
    Keep note of the install location "Location" as you will need it in the steps below.

__Go to Xailient Installation Folder__

To go to xailient folder, use the following command. If you do not know the install location, please refer to __"Info about xailient sdk installed"__ section above.

```bash
(env) $ cd <Xailient Install Location>/xailient
```

__Xailient SDK contents__

```bash
(env) $ ls
```

* bin/ -- Executables required for initial registration
* data/ -- Image files you can use with the sample applications
* samples/ -- Sample application demonstrating how the Xailient SDK library can be used
* scripts/ -- License activation scripts
* sharedLib_x86_64/ --Sample models that can be installed or linked with your applications


__Install tflite runtime__

Install the tflite runtime using requirements.txt file.

```bash
(env) $ python3.7 -m pip install -r requirements.txt
```

__Activate your license__

Go to __scripts__ folder and execute xailient-install script

```bash
(env) $ cd scripts
(env) $ sudo ./xailient-install
```

## Run sample code

In the xailient folder of the install location, go to __samples__ folder. This folder contains a sample python script named "basic_sample.py" that demonstrates how to use the xailient sdk. 

The script reads an image named "beatles.jpg" from __data__ folder, runs the detection sdk on this image and saves output to "beatles_output.jpg" in the same folder.

Before we can run this script, we need to ensure that we give the OPTIMAL THRESHOLD.

Go to the Console, navigate to __MANAGE AI MODELS__ and click on the model which you have installed. 
Scroll down to __Evaluation Results__ where you can find __BEST THRESHOLD__.

<p align="center">
  <img src="../img/console/Evaluation_thresh.png">
</p>

Then using a text editor of your choice, edit the basic_sample.py script to include the value for __BEST THRESHOLD__ as found above.

<p align="center">
  <img src="../img/console/best_thresh.png">
</p>

Now run the sample script.


```bash
(env) $ cd ../samples
(env) $ python3.7 basic_sample.py
```

Now go to __data__ folder to see the input and output images.

Input Image | Output Image
:-------------------------:|:-------------------------:
![](../img/x86_64/beatles.jpg)   |  ![](../img/x86_64/beatles_output.jpg)


## Update Xailient SDK Model

```bash
(env) $ python3.7 -m pip uninstall xailient
(env) $ python3.7 -m pip install "<new SDK WHEEL URL>"
```

When you install a new SDK with a different model using pip install, you do not need to run the licence activation script again.

## Uninstall Xailient

Go to xailient/scripts folder and run the uninstalltion script.

``` bash
(env) $ ../scripts
(env) $ sudo ./xailient-uninstall
```

Pip uninstall xailient

```bash
(env) $ python3.7 -m pip uninstall xailient
```

Keep in mind that after uninstall, the data folder and sample folder will remain.
When you install a new SDK with a different model, these folders will be reintegrated into the SDK. This allows users to easily move data and scripts across different SDKs.

Note that any changes to the basic_sample.py python script will be overwritten so keep a backup if you intend to keep any changes.

