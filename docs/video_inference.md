# Evaluate your AI

<!-- blank line -->
<figure class="video_container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/u5tYxLGTh7E?start=373" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
<!-- blank line -->

One cool feature in Xailient Console is that you can test your model quickly. By uploading a wild video and you can get a processed video with inferences of the trained AI model.

That means that you don't have to go through the whole process of deploying your AI model on your device inorder to see how it performs.

## Evaluation on Images

Once the model training is completed successfully, you can see its predictions on a held out set of images from your dataset.

To view the images, from __AI Models__ page, click on the successfully trained model.

<p align="center">
<img src="../latest/img/console/AI Models/PretrainedAIModels-ListSelectModel.png">
</p>

<p align="center">
<img src="../latest/img/console/AI Models/InferenceOnHeldOutImage-2.png">
</p>

## Video Inference

1. From the navigation menu on the left, under __AI Models__ click __View__ for Custom Trained models and __Pre-trained__ for pre-trained models.

    <p align="center">
    <img src="../latest/img/console/Dashboard/LeftMenu-PretrainedAI.png" width="250">
    </p>

2. For a model that has completed training, and the status is __Success__, click on the <img src="../latest/img/console/AI Models/UploadVideoButton.png" height=30 width=30> icon.

    <p align="center">
    <img src="../latest/img/console/AI Models/PreTrainedModels-SDKBuilt-Video.png">
    </p>

3. Select the video (must be in mp4 format) that you wish to upload and click __UPLOAD__ button.

    <p align="center">
    <img src="../latest/img/console/AI Models/VideoInference-UploadVideo.png">
    </p>

4. When the video upload is completed, it will be listed under __Select Uploaded Videos__.

5. From __Select Upload Videos__ list, select the video which you want to process using the AI model and click __PROCESS VIDEO__.

    <p align="center">
    <img src="../latest/img/console/AI Models/VideoInference-SelectAndProcess.png">
    </p>
6.  When the video processing begins, it will be listed under __Status of processing predictions__ list. It will take a couple of munited for the processing to complete.

    <p align="center">
    <img src="../latest/img/console/AI Models/VideoInference-InProgress.png">
    </p>

7. Once it is complete, the processed video will be listed under __Videos with predictions__. To video the processed video, click the __VIEW PROCESSED VIDEO__ icon. A new tab in your broswer will be opened with the video. 

    <p align="center">
    <img src="../latest/img/console/AI Models/VideoInference-Processed.png">
    </p>

