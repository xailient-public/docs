# Train your own AI Models

<!-- blank line -->
<figure class="video_container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/o7rsZ6hvxvk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
<!-- blank line -->

With Xailient Console, you can train custom AI models, which you can then deploy to your targeted devices.

To train any AI model, you will need training data. 

Xailient Console comes with pre-loaded public datasets.

You can either use the pre-loaded datasets, upload your own dataset, or combine different datasets inorder to train your AI.

## Pre-loaded Dataset

From the navigation menu on the left, go to __MANAGE DATASETS__.

<p align="center">
  <img src="../img/console/nav_dataset_list.png">
</p>

Under __Pre-loaded Public Datasets__ you will see a list of all the public datasets that we have pre-loaded and made available to you.

<p align="center">
  <img src="../img/console/PreloadedDataset.png">
</p>

## Upload your own Dataset

1. To prepare your images for uploading to the Console, place all the images into a folder. All images must be either in .jpg or .png format. 

2. Now compress the folder into a .zip or .gz file. 

3. Prepare labels for your dataset in CSV format. Please ensure your CSV has only these SIX columns. Spelling matters and it's case sensitive. The order doesn't matter. 
    
    __E.g. ['image_name', 'class', 'xmin', 'ymin', 'xmax', 'ymax']__

    Here is what the CSV file should look like:

    <p align="center">
    <img src="../img/console/PrepareLabel.png">
    </p>
 

3. Go to the Console. From the navigation menu on the left, go to __ADD NEW DATASETS__.

    <p align="center">
    <img src="../img/console/nav_add_dataset.png">
    </p>

4. Enter the name of the dataset, select the zip file yor prepared eariler and click __UPLOAD__.

    <p align="center">
    <img src="../img/console/AddDataset.png">
    </p>

5. When the upload begins, do not close the browser to ensure that the dataset is uploaded successfully.

    <p align="center">
    <img src="../img/console/DatasetUploadInProgress.png">
    </p>

6. Now upload your label file you prepared earlier.

    <p align="center">
    <img src="../img/console/UploadLabel.png">
    </p>

7. When the lable file upload is completed, you will then get redirected to __MANAGE DATASETS__ page where your dataset is currently getting sanity checked before it becomes available. This can take a few minutes. Refresh the page if it takes longer than 20 minutes!

    <p align="center">
    <img src="../img/console/Dataset_sanity_begin.png">
    </p>

    If the sanity check passes without errors, it will get automatically listed to the above list and will now be ready to train on. 

    <p align="center">
    <img src="../img/console/DatasetReady.png">
    </p>

    If the sanity check fails then the ERROR DETAILS could explain the reason. For example, here we have uploaded a CSV labels file where not a single image in the .zip file has a corresponding annotation. So make sure at least 1 row in the CSV file corresponds to an image filename in the .zip file. You can correct these errors and re-upload the CSV by clicking __UPDATE LABEL__.

    <p align="center">
    <img src="../img/console/Sanity_error.png">
    </p>


    Sometimes the sanity check will pass with partial success because we detected that some images don’t contain labels and vice versa, which is acceptable since this means the rest have corresponding labels. In this case you acknowledge the error and can manually approve it by clicking the __APPROVE__ button.
    
    <p align="center">
    <img src="../img/console/Partial-success.png">
    </p>

    This approved dataset will then get listed above and is now ready to train on.

    <p align="center">
    <img src="../img/console/DatasetReady.png">
    </p>


## Train your AI

1. To train an AI model, navigate to __TRAIN NEW AI MODEL__ from the menu on the left.

2. Select dataset(s) by ticking the box(es). You can select a single or combine multiple (both public and private) datasets to train a model.

    <p align="center">
    <img src="../img/console/Train_combined.png">
    </p>

3. You can further select only specific subclasses within the (set of) datasets. A single model will train on the combined datasets and predict only those classes you have chosen here.

    <p align="center">
    <img src="../img/console/CombineClass2.png">
    </p>

4. Enter model name for your AI model.

    <p align="center">
    <img src="../img/console/ModelName.png">
    </p>

5. Select a value for __Speed vs Accuracy__ between 1 to 5. 

    <p align="center">
    <img src="../img/console/SpeedVsAccuracy.png">
    </p>

    __1__ is the fastest. It is best for larger objects with simple backgrounds. You should select option 1 if your objects of interest are medium to big (close range).


    __2__ is slower than 1 and should be used if your objects of interest are small to medium (medium range).


    __3__ is slower than 2 and should be used if your objects of interest are small (long range).


    __4__ is slower than 3 and should be used if your objects of interest are smaller and background is complex (longer range).


    __5__ is the slowest. It is best for smaller objects with complex backgrounds. You should use option 5 if your objects of interest are very small and background is complex (longest range).

5. Begin training by clicking __BEGIN TRAINING__.

    <p align="center">
    <img src="../img/console/BeginTraining.png">
    </p>

    <p align="center">
    <img src="../img/console/TrainingStarted.png">
    </p>


## View Training Status

To view the training status of your AI model, navigate to __MANAGE AI MODELS__, and find your model under __Training Models__. Once the training is completed, you will get an email notification regarding it.

<p align="center">
<img src="../img/console/TrainingInProgress.png">
</p>

## Deploy your AI

When the training is complete, you can build an SDK and install it on the targeted device. For more details on how to build an SDK, refer to [Build Deployable SDK](/en/latest/buildSdk/) section of the documentation

For instructions on how to setup your device, install the SDK and run it, please refer to [Deploy You AI](/en/latest/installation/) section of the documentation.