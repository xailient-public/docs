# Evaluate your AI

One cool feature in Xailient Console is that you can test your model quickly. By uploading a wild video and you can get a processed video with inferences of the trained AI model.

That means that you don't have to go through the whole process of deploying your AI model on your device inorder to see how it performs.

## Evaluation on Images

Once the model training is completed successfully, you can see its predictions on a held out set of images from your dataset.

To view the images, from __MANAGE AI MODEL__ page, click on the successfully trained model.

<p align="center">
<img src="../img/console/Evaluation.png">
</p>

## Video Inference

1. From the navigation menu on the left, go to __MANAGE AI MODEL__.

    <p align="center">
    <img src="../img/console/nav_list_models.png">
    </p>

2. Under __Training Models__ you will see a list of all the models that are inprogress and that have completed training.

    For a model that has completed training, and the status is __Success__, click on the __Upload Video__ icon.

    <p align="center">
    <img src="../img/console/TrainedModel_uploadVideo.png">
    </p>

3. Select the video (must be in mp4 format) that you wish to upload and click __UPLOAD__ button.

    <p align="center">
    <img src="../img/console/VideoUpload.png">
    </p>

4. When the video upload is completed, it will be listed under __Select Uploaded Videos__.

    <p align="center">
    <img src="../img/console/SelectVideos.png">
    </p>

1. From __Select Upload Videos__ list, select the video which you want to process using the AI model and click __PROCESS VIDEO__.

    <p align="center">
    <img src="../img/console/ProcessVideo.png">
    </p>

2.  When the video processing begins, it will be listed under __Status of processing predictions__ list. It will take a couple of munited for the processing to complete.

    <p align="center">
    <img src="../img/console/VideoInProgress.png">
    </p>

3. Once it is complete, the processed video will be listed under __Videos with predictions__. To video the processed video, click the __VIEW PROCESSED VIDEO__ icon. A new tab in your broswer will be opened with the video. 

    <p align="center">
    <img src="../img/console/VideoWithPredictions.png">
    </p>

