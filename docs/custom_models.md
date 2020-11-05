# Train your own AI Models

<!-- blank line -->
<figure class="video_container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/o7rsZ6hvxvk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
<!-- blank line -->

With Xailient Console, you can train custom AI models, which you can then deploy to your targeted devices.

To train any AI model, you will need training data. 

Xailient Console comes with pre-loaded public datasets.

You can either use the [pre-loaded datasets](https://xailient-docs.readthedocs.io/en/latest/dataset/), [upload your own dataset](https://xailient-docs.readthedocs.io/en/latest/dataset/), or combine different datasets inorder to train your AI.

## Select Dataset(s)

1. To train an AI model, from the left menu, under __AI Models__ click __Add__.

2. Select dataset(s) by ticking the box(es). You can select a single or combine multiple (both public and private) datasets to train a model.

    <p align="center">
    <img src="../img/console/AI Models/TrainAI-Step1-DatasetSetected.png">
    </p>

## Select Class(es)

3. Enter model name for your AI model.

4. You can further select only specific subclasses within the (set of) datasets. A single model will train on the combined datasets and predict only those classes you have chosen here.

    <p align="center">
    <img src="../img/console/AI Models/TrainAIModel-Step2.png">
    </p>

## Select type of AI model

5. Select a value for __Speed vs Accuracy__ between 1 to 5. 

    <p align="center">
    <img src="../img/console/SpeedVsAccuracy.png">
    </p>

    __1__ is the fastest. It is best for larger objects with simple backgrounds. You should select option 1 if your objects of interest are medium to big (close range).


    __2__ is slower than 1 and should be used if your objects of interest are small to medium (medium range).


    __3__ is slower than 2 and should be used if your objects of interest are small (long range).


    __4__ is slower than 3 and should be used if your objects of interest are smaller and background is complex (longer range).


    __5__ is the slowest. It is best for smaller objects with complex backgrounds. You should use option 5 if your objects of interest are very small and background is complex (longest range).

## Begin Training

5. Begin training by clicking __BEGIN TRAINING__.

    <p align="center">
    <img src="../img/console/BeginTraining.png">
    </p>

    <p align="center">
    <img src="../img/console/TrainingStarted.png">
    </p>

## View Training Status

To view the training status of your AI model, under __AI Models__ click __View__, and find your model under __Training Models__. Once the training is completed, you will get an email notification regarding it.

<p align="center">
<img src="../img/console/Dashboard/LeftMenu-CustomAIModels.png" width="250">
</p>


<p align="center">
<img src="../img/console/AI Models/CustomAIModels-List-InProgress.png">
</p>

## Deploy your AI

When the training is complete, you can build an SDK and install it on the targeted device. For more details on how to build an SDK, refer to [Build Deployable SDK](/en/latest/buildSdk/) section of the documentation

For instructions on how to setup your device, install the SDK and run it, please refer to [Deploy You AI](/en/latest/installation/) section of the documentation.

If your local machines doesn't meet the requirements for native installation we also offer Docker [Containers as a deployment option](https://xailient-docs.readthedocs.io/en/latest/container/).