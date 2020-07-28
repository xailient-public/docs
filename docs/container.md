<p align="center">
  <img src="../img/container/docker_xailient.png">
</p>
<br>
We also offer Docker Containers as an option to deploy your trained models from your desktop.
This option is currently in beta but is a great way to test the Xailient SDK without worrying about the installation process or the requirements of your machine.

We recommend this option for users who don't meet the requirements for native installation however are able to run the Docker application.

The latest version of our container enables users to **batch process images** using their own custom trained model.

## Download Docker
New to Docker and containerisation?

* [Downloads](https://www.docker.com/products/docker-desktop)
* [Find out more about container technology](https://www.docker.com/resources/what-container)

<br>
## Downloading a Xailient Image
Run the following command to pull our latest image from Docker Hub

`$ docker pull xailient/model-inference`

If successful run `$ docker images` and check if the image "xailent/model-inference" appears in the list.

<br>
## Starting a Xailient SDK instance
### Setup
On your local machine create a directory called "test" and then create two further subdirectories called "input" and "output". 

<p align="center">
  <img src="../img/container/test.png">
</p>

Place any images you want to run inference on in the subdirectory called "input".
The "test" directory will be mounted into your Container when you run it. 

We will explain how to do this later.

<br>
Before running the Container, you must first **ensure you have a trained model** to use.
You can either:

1. Train a custom model
2. Use a pretrained model

To achieve this follow the steps at [Training a model](custom_models.md)

Next you will need to [Build Deployable SDK](buildSdk.md) and choose the **X86-64** option

<br>
### Running the container
First step here is to obtain an SDK_LINK from the training console.

Go to __MANAGE AI MODELS__ page and locate the model for which you have build the SDK.

Click on __Download/Copy SDK__ button for that model. 

<p align="center">
<img src="../img/console/SDKBuildComplete.png" heigth=100>
</p>

A link will be copied to your clipboard. If a download occurs you can ignore or cancel it.

<br>
Finally run,

`$ docker run -e SDK_LINK='<LINK>' -v <test_path>:/app/volume xailient/model-inference`

- Replace `<LINK>` with the SDK link obtained earlier. Here you are passing the link to the container as an environment variable.
- Replace `<TEST_PATH>` with the **full path** to the directory named "test", which we created earlier. Here we are mounting a local directory to the Container as a volume. In other words, giving the Container access to a directory on our local machine.

**Example:**

`$ docker run -e SDK_LINK='https://ReallyLongUrl/AAaDDY2MzE1ODQ0NzQx' -v /Users/Bernie/Desktop/test:/app/volume xailient/model-inference`

All predictions will appear in the "output" subdirectory.


<br>
## Further options
### Thresholding
Play around with different thresholds by passing in the environment variable THRESHOLD when running the container instance. E.g.

**Example:**
`$ docker run -e THRESHOLD='0.8' -e SDK_LINK='<LINK>' -v <test_path>:/app/volume xailient/model-inference`

### Output bounding box coordinates
You can also output textfile called log_output.txt which lists the bouding box coordinates of each prediction for an image.
Achieve this by passing the boolean environment variable LOG.

**Example:**
`$ docker run -e LOG='True' -e SDK_LINK='<LINK>' -v <test_path>:/app/volume xailient/model-inference`