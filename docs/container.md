<p align="center">
  <img src="../img/container/docker_xailient.png">
</p>
<br>

While the Xailient SDK is designed to provide state of the art machine vision performance efficient enough to run on
low power IoT devices using technology inspired by human biology, we also offer a Docker container as an option to
deploy your trained models from your desktop.
This option is a great way to see the Xailient SDK in action using a desktop OS like Mac or Windows.

We recommend this option for users who don't have access to an IoT device or Linux VM, or that simply want to be able to use a Xailient SDK from their Mac or Windows computers.

The latest version (1.0.1) of our container enables users to **batch process images and videos** using their own custom trained model.

## Overview of the Xailient SDK Container 

The Xailient SDK container makes it easy to see the bounding boxes predicted by the Xailient SDK on a set of images or videos
of your choosing. Simply start the Xailient SDK container by pointing it to an input directory full of images or videos and it will
populate the output directory with images and/or videos with predicted bounding boxes drawn on each image (or frame of video).

When processing videos you can choose to have the Xailient SDK container output each frame of the video as an image (with bounding
boxes drawn of course!). Or you can choose to have it output a video so you can see what the Xailient SDK might look like in
real time.

<br>
## Using the Xailient SDK Container

First, [download and install Docker Desktop](https://www.docker.com/products/docker-desktop).

Next, you must **ensure you have a trained model** to use.
You can either:

1. Use a [pretrained model](https://console.xailient.com/user/listModel) available in the Xailient console, OR
2. Train a custom model. To achieve this follow the steps at [Training a model](custom_models.md).

Next you will need to [Build a Xailient SDK](buildSdk.md) and choose the **X86-64** option.

<br>
### Obtaining a Link to a Xailient SDK

Go to the [MANAGE AI MODEL page](https://console.xailient.com/user/listModel) and locate the model for which you have built the SDK.

Click on __Download/Copy SDK__ button for that model. 

<p align="center">
<img src="../img/console/SDKBuildComplete.png" heigth=100>
</p>

A link will be copied to your clipboard and a download will begin.

<br>
## Run the Xailient SDK Container

    `$ docker run -e SDK_LINK="<LINK>" -v <INPUT_IMAGES_DIR>:/input -v <OUTPUT_IMAGES_DIR>:/output xailient/model-inference:1.0.1`

Replace `<LINK>` with the SDK link obtained earlier. Here you are passing the link to the container as an environment variable.
Be sure to include __double quotes around the SDK download link__ since the link may contain characters like `&` that can cause problems if not quoted.

Replace `<INPUT_IMAGES_DIR>` with the __full path__ to the directory that has your images and/or videos that you want to
run through the Xailient SDK.

Replace `<OUTPUT_IMAGES_DIR>` with the __full path__ to a directory where the images and videos with their predicted bounding
boxes drawn will be placed.

Note: You can also place the downloaded Xailient SDK (a python .whl file) into the `<INPUT_IMAGES_DIR> ` directory of the host OS.
 Then you can start the docker container without specifying the Xailient SDK's URL via `-e SDK_LINK="<LINK>"` e.g.

    `$ docker run -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

Providing an `SDK_LINK` takes precedence over placing the Xailient SDK file in the "input" directory. Therefore, be aware when swapping in different Xailient SDKs.

**Example:**

    `$ docker run -e SDK_LINK="https://ReallyLongUrl/AAaDDY2MzE1ODQ0NzQx" -v ~/Desktop/input:/input -v ~/Workspace/output:/output xailient/model-inference:1.0.1`

In this example, all predicted images and videos will appear in the `~/Workspace/output` of the host OS.

<br>
## Default Behaviour

By default the Xailient SDK container will output images for all given input images, and output videos and their frames for all given input videos.

* Supported Image formats: jpeg/jpg, png
* Supported Video formats: mp4, avi, flv, mkv, mov, webm, wmv

It will also create a csv file named "predictions.csv" with rows corresponding to the bounding box coordinates for each image.

This default behavior can be changed with the following options. Each option is controlled via an environment variable that
gets passed to the `docker run` command. See below for examples of how to use these options.

<br>
## Supported Options

### IMAGES (default=True)
Controls whether images with predicted bounding boxes are created in the output directory for input images. Also controls whether individual video frames appear with bounding boxes.
To disable this set the environment variable IMAGES to False.

**Example:**
`$ docker run -e IMAGES=False -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### REBUILD (default=True)
Controls whether videos with predicted bounding boxes are created in the output directory for input videos.
See the `FPS` and `EVERY` option for even more control over the output video that gets created.

**Example:**
`$ docker run -e REBUILD=True -e EVERY=20  -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### EVERY (default=1)
Perform inference on every ith frame of all given videos.

**Example:**
`$ docker run -e EVERY=20 -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### FPS (defaults to the original video fps)
Reconstructed videos will have this many frames per second.

**Example:**
`$ docker run -e FPS=30 -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### THRESHOLD (default=Optimal)
Optimal threshold determined during training and built into the SDK Model.
Note for SDK model version 1.0.4 the default is 0.25.

Play around with different confidence thresholds by passing in the environment variable THRESHOLD when running the Container instance. Accepts floating values from 0 to 1.

**Example:**
`$ docker run -e THRESHOLD='0.8' -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

### LOG (default=True)
Controls whether a .csv file with bounding boxes for all predicted images is created in the output directory.
To disable this set the environment variable LOG to False.

**Example:**
`$ docker run -e LOG=False -v <FULL_PATH>:/input -v <FULL_PATH>:/output xailient/model-inference:1.0.1`

<br>
## Releases

`1.0.1`

Enables users to batch process images and videos using their own custom trained model.

<br>
## Common Problems
1. Check that you have used the fullpath to your input and output directories. The Container will still run if you use relative paths however will not work as intended. I.e. Video/image inferencing will **not** work.
2. Check that you have used double quotations " " around the SDK_LINK. Since the link may contain characters like `&` that can cause problems if not quoted.

