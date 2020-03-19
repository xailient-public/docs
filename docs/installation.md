# Getting Started

*NOTE: This version of the documentation is for installation of Xailient SDK using wheel file (.wh). 
If you are looking for documentation for installion of Xailient SDK using SDK package, please visit our old [documentation](https://xailient.readthedocs.io/en/latest/installation/).*

## Device Setup

To meet the minimum requirements, your device must be a x86_64 architecture device. We’ve tested the following operating systems:

* Ubuntu 18.04 LTS

__Minimum software requirements:__

* Python3.7
* Pip for python3.7
* OpenCV

If your device does not meet the minimum software required, please follow the instructions below to install them.

__Download the package lists and update information__

<pre><code>sudo apt-get update</code></pre>

![](img/apt_update.png)

*NOTE: apt-get update to download the package lists from the repositories and "update" them to get information on the newest versions of packages and their dependencies. It will do this for all repositories and PPAs.*

__Install python3.7__

<pre><code>sudo apt-get install python3.7</code></pre>

![](../img/install_python.png)

__Install pip for python3.7__

<pre><code>sudo apt-get install python3-pip</code></pre>

![](../img/install_pip.png)

__Install OpenCV__
<pre><code>sudo apt-get install python-opencv</code></pre>

![](../img/install_opencv.png)

## Install XailientSDK

__Check if python 3.7 is installed__

![](../img/check_python.png)

If python3.7 is not installed, please refer to Device Setup to install it.

__Check if pip for python3.7 is installed__

![](../img/check_pip.png)

If pip for python3.7 is not installed, please refer to Device Setup to install it.

*NOTE: In 18.04 Ubuntu, by default __pip3__ is for python3.6. So we will use __python3.7 -m pip__ command instead to use pip for python3.7.
If pip3 for your device defaults to python3.7, feel free to replace the command __python3.7 -m pip__ with __pip3__.*

__Install SDK Wheel__

<pre><code>python3.7 -m pip install “&lt;SDK WHEEL URL&gt;”</code></pre>

*NOTE: Replace &lt;SDK WHEEL URL&gt; with your wheel url.*

![](../img/install_xailient.png)

__Info about xailient sdk installed__

<pre><code>python3.7 -m pip show xailient</code></pre>

![](../img/check_xailient.png)

You can get information about the version of xailient sdk installed, support email address, and location of the installation. 

__Xailient SDK contents__

* bin/ -- Executables required for initial registration
* data/ -- Image files you can use with the sample applications
* samples/ -- Sample application demonstrating how the Xailient SDK library can be used
* scripts/ -- License activation scripts
* sharedLib_x86_64/ --Sample models that can be installed or linked with your applications

__Install tflite runtime__

Go to xailient folder and install the tflite runtime using requirements.txt file.

<pre><code>python3.7 -m pip install -r requirements.txt</code></pre>

__Activate your license__

In xailient folder of the install location, go to scripts folder and execute xailient-install script

![](../img/scripts_folder.png)

<pre><code>sudo ./xailient-install</code></pre>

![](../img/activate_license.png)

## Run sample code

In the xailient folder of the install location, go to samples folder. This folder contains a sample python script named “basic_samples.py” that demonstrates how to use the xailient sdk. 

![](../img/sample_folder.png)

The script reads an image named “beatles.jpg” from xailient/data folder, runs the detection sdk on this image and saves output to “beatles_output.jpg” in the same folder.

<pre><code>python3.7 basic_samples.py</code></pre>

![](../img/run_sample_code.png)

Now go to xailient/data folder to see the input and output images.

Input Image | Output Image
:-------------------------:|:-------------------------:
![](../img/beatles.jpg)   |  ![](../img/beatles_output.jpg)


## Uninstall Xailient

<pre><code>python3.7 -m pip uninstall xailient</code></pre>

