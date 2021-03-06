# Multi Class Object Detector

Multi Class Object Detector is used when you want to detect and identify multiple classes of objects in one or more images.

<p align="center">
<figure>
  <img src="../latest/img/console/AI Models/multiclass_object_detection.png">
  <figcaption>Multi-class Object Detection <a href="https://miro.medium.com/max/1400/0*IW_DpAtoCrDBVhdO.png">(Source)</a></figcaption>
</figure>
</p>


In Xailient Console, you can train two popular multi-class object detectors:

1. [SSD](https://arxiv.org/abs/1512.02325)
2. [YOLO](https://arxiv.org/abs/1804.02767)

To train a multi-class object detector with SSD architecture, you can either use the default training setting or define your own.

The training configuration file gives you full control of the hyperparameters for the trainng.

These are the settings you can modify:

* __batch_size__: The batch size is a number of samples processed before the model is updated. The size of a batch must be more than or equal to one and less than or equal to the number of samples in the training dataset.

* __epochs__: The number of epochs is the number of complete passes through the training dataset.  The number of epochs can be set to an integer value between one and infinity.

* __augment_multiplier__: You can use this setting to augment your training data. 1 means add 1x to the dataset (double it). 2 means add 2x (triple it).

We recommend keeping all the other setting to default.

### SSD

Here is a sample configuration for the SSD architeture. 

``` yml
data:
  reshape_dim: 300
  tile_dim: 300

train:
  model_arch: 'MobileNetV2SSD'
  batch_size: 32
  epochs: 200
  augment_multiplier: 0 # 1 means add 1x to the dataset (double it). 2 means add 2x (triple it).
  classes: 'all'
  encoding_iou_threshold: 0.5  # The IoU that will be used to match ground truth to priors when encoding
  min_area: 0
  # one of the aspect ratios has to be 1, the aspect ratios determine how many
  # anchor boxes will be generated for each location on every prediction feature map
  aspect_ratios: [1.0, 2.0, 0.5, 3.0, 0.3]  # The aspect ratios implemented in the original SSD paper.
  l2_regularization: 1.0e-3

loss:
  neg_pos_ratio: 3  # Used for hard negative mining. Ratio of negatives to positives.
  alpha: 1.0  # Used as a factor to multiply localization loss by in multi-box loss.

optimizer:
  name: 'Adam'
  params:
    lr: 1.0e-3

inference:
  probability_threshold: 0.1
  nms_max_iou: 0.45
```

### YOLO

Here is a sample configuration for the YOLO architeture. 

``` yml
train:
  batch_size: 64
  epochs: 12
  generate_anchor: false
```