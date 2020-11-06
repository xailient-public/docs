# Datasets

With Xailient Console, you can can either use the pre-loaded datasets, upload your own dataset, or combine different datasets inorder to train your AI.

## Pre-loaded Dataset

From the navigation menu on the left, under __Datasets__ click __Pre-Loaded__.

<p align="center">
  <img src="../img/console/Dashboard/LeftMenu-Preloadeddataset.png" width="250">
</p>

Here, you will see a list of all the public datasets that we have pre-loaded and made available to you.

<p align="center">
  <img src="../img/console/Dataset/PreLoadedDatasetList.png">
</p>

## Upload your own Dataset

1. To prepare your images for uploading to the Console, place all the images into a folder. All images must be either in .jpg or .png format. 

2. Now compress the folder into a .zip or .gz file. 

3. Prepare labels for your dataset in CSV format. Please ensure your CSV has only these SIX columns. Spelling matters and it's case sensitive. The order doesn't matter. 
    
    __E.g. ['image_name', 'class', 'xmin', 'ymin', 'xmax', 'ymax']__

    Here is what the CSV file should look like:

    <p align="center">
    <img src="../img/console/Dataset/PrepareLabel.png">
    </p>
 

3. Go to the Console. From the navigation menu on the left, under __Dataset__ click __Add__.

    <p align="center">
    <img src="../img/console/Dashboard/LeftMenu-AddDataset.png" width="250">
    </p>

4. Enter the name of the dataset, select the zip file yor prepared eariler and click __UPLOAD__.

    <p align="center">
    <img src="../img/console/Dataset/UploadDataset-Step1.1.png">
    </p>

5. When the upload begins, do not close the browser to ensure that the dataset is uploaded successfully.

    <p align="center">
    <img src="../img/console/Dataset/UploadingDataset.png" width="350">
    </p>

    <p align="center">
    <img src="../img/console/Dataset/DatasetUploadedSuccessfully.png" width="350">
    </p>
    

6. Now upload your label file you prepared earlier.

    <p align="center">
    <img src="../img/console/Dataset/UploadDataset-Step2.png">
    </p>

7. When the lable file upload is completed, you will then get redirected to __MANAGE DATASETS__ page where your dataset is currently getting sanity checked before it becomes available. This can take a few minutes. Refresh the page if it takes longer than 20 minutes!

    <p align="center">
    <img src="../img/console/Dataset/DatasetSanityCheckStarted.png">
    </p>

    If the sanity check passes without errors, it will get automatically listed to the above list and will now be ready to train on. 

    <p align="center">
    <img src="../img/console/Dataset/MyDatasets.png">
    </p>

    If the sanity check fails then the ERROR DETAILS could explain the reason. For example, here we have uploaded a CSV labels file where not a single image in the .zip file has a corresponding annotation. So make sure at least 1 row in the CSV file corresponds to an image filename in the .zip file. You can correct these errors and re-upload the CSV by clicking __UPDATE LABEL__.

    <p align="center">
    <img src="../img/console/Dataset/SanityCheckResult-Error.png">
    </p>


    Sometimes the sanity check will pass with partial success because we detected that some images don't contain labels and vice versa, which is acceptable since this means the rest have corresponding labels. In this case you acknowledge the error and can manually approve it by clicking the __APPROVE__ button.
    
    <p align="center">
    <img src="../img/console/Dataset/SanityCheckResult-PartialSuccess.png">
    </p>

    This approved dataset will then get listed above and is now ready to train on.

    <p align="center">
    <img src="../img/console/Dataset/MyDatasets.png">
    </p>
