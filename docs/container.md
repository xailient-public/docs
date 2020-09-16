<p align="center">
  <img src="../img/container/docker_xailient.png">
</p>
<br>

We also offer Docker Containers as an option to deploy your trained models from your desktop.
This option is a great way to test the Xailient SDK without worrying about the installation process or the requirements of your machine.

We recommend this option for users who don't meet the requirements for native installation however are able to run the Docker application.

The latest version of our container enables users to **batch process images and videos** using their own custom trained model.

## Download Docker
New to Docker and containerisation?

* [Download Docker Desktop](https://www.docker.com/products/docker-desktop)
* [Find out more about container technology](https://www.docker.com/resources/what-container)

<br>
## Downloading a Xailient Image
Run the following command to pull our latest image from Docker Hub

`$ docker pull xailient/model-inference:1.0.1`

If successful run `$ docker images` and check if the image "xailent/model-inference" appears in the list.

<br>
## Starting a Xailient SDK instance
### Setup
- On your local machine create two directories called "input" and "output". 
- Place any images or videos you want to run inference on in the directory called "input".

<br>
Before running the Container, you must first **ensure you have a trained model** to use.
You can either:

1. Train a custom model
2. Use a pretrained model

To achieve this follow the steps at [Training a model](custom_models.md)

Next you will need to [Build Deployable SDK](buildSdk.md) and choose the **X86-64** option

<br>
### Running the container
First step here is to copy an SDK_LINK or download the SDK wheel file (.whl) from the training console.

Go to __MANAGE AI MODELS__ page and locate the model for which you have build the SDK.

Click on __Download/Copy SDK__ button for that model. 

<p align="center">
<img src="../img/console/SDKBuildComplete.png" heigth=100>
</p>

A link will be copied to your clipboard and a download will begin.

<br>
To run the container either,

A. Pass the SDK_LINK you copied earlier as an environment variable.

  `$ docker run -e SDK_LINK="<LINK>" -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

B. Place the downloaded SDK wheel file into the "input" directory instead of using the link.

`$ docker run -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

**Note:**

- Replace `<LINK>` with the SDK link obtained earlier. Here you are passing the link to the container as an environment variable.
- Replace `<FULL_PATH>` with the **full path** to the directories "input" and "output", which we created earlier. Here we are mounting local directories to the Container as a volume. In other words, giving the Container access to a directory on the local machine.
- Providing an SDK_LINK takes precedence over placing the SDK wheel file in the "input" directory. Therefore, be aware when swapping in different models.

**Example:**

`$ docker run -e SDK_LINK="https://ReallyLongUrl/AAaDDY2MzE1ODQ0NzQx" -v ~/Desktop/input:/input -v ~/Workspace/output:/output xailient/model-inference:1.0.1`

All predictions will appear in the "output" directory.

<br>
## Default Behaviour

Placing the following in the "input" directory:

- SDK wheel file: xailient-1.0.4-py3-none-linux_x86_64.whl
- An image called car.jpeg
- A video of called traffic.mp4

and running 
`$ docker run -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

You will find in the output directory:

- A csv file named "predictions.csv" with rows corresponding to the bounding box coordinates for each image.
- car_output.jpeg with bounding boxes drawn.
- Further images with bounding boxes which correspond to the frames from the video file traffic.mp4

<br>
## Further options
### Thresholding
Play around with different thresholds by passing in the environment variable THRESHOLD when running the Container instance. E.g.

**Example:**
`$ docker run -e THRESHOLD='0.8' -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### Perform inference on every ith frame of all given videos
As an example, you could perform inference on every 20th frame in a video with the environment variable EVERY.

**Example:**
`$ docker run -e EVERY=20 -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### Reconstruct videos with bounding boxes on each frame.
You can output the original videos with bounding boxes drawn on each frame with the environment variable REBUILD. You can also pass another variable FPS to set the framerate, default is 2.

This functionality can be combined with choosing the ith frame to do inference with the EVERY option above.

**Example:**
`$ docker run -e EVERY=20 -e REBUILD=True -e FPS=10 -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### Disable output of all images
Achieve this by setting the boolean environment variable IMAGES to False.
Note that this will also disable the REBUILD option for videos.

**Example:**
`$ docker run -e IMAGES=False -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### Disable predictions.csv output
Achieve this by setting the boolean environment variable LOG to False.

**Example:**
`$ docker run -e LOG=False -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

