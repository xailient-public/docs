# Selective Attention Network

To train a Selective Attention Model, you can either use the default training setting or define your own.

### Selecting Training Settings Using Slider Bar

If you are in __"Free"__ or __"Premium"__ subscription, you can control the training settings using a slider bar.

<p align="center">
<img src="../latest/img/console/AI Models/Training-Config-SliderBar.png">
</p>

Select a value for __Inference Speed vs Accuracy__. 

!!! note
    __1__ is the fastest. It is best for larger objects with simple backgrounds. You should select option 1 if your objects of interest are medium to big (close range).

    __2__ is slower than 1 and should be used if your objects of interest are small to medium (medium range).


### Selecting Training Settings Using Configuration File

If you are in __"Admin"__ subscription, you can upload a training configuration file to defie the training settings. The training configuration file gives you full control of the hyperparameters for the training.

<p align="center">
  <img src="../latest/img/console/AI Models/Training-Config-Upload.png">
</p>

These are the settings you can modify:

* __data -> input_dim__: input_dim is the input resolution to the network to be trained. The input_dim must be a multiple of 32. Minimum value is 64 and maximum value is 1024. For e.g. 64, 96, 128, 160, ..., 1024.

!!! Guide
    * Use 64 if your objects of interest are large sizes (e.g. faces up to 1 m away or vehicles up to 5 m away).
    * Use 128 if your objects of interest are small to medium sizes (e.g. faces up to 3 m away or vehicles up to 20 m away).
    * Use 256 if your objects of interest are tiny sizes (e.g. faces up to 10 m away or vehicles up to 200 m away).

* __train -> batch_size__: The batch size is a number of samples processed before the model is updated. The size of a batch must be more than or equal to one and less than or equal to the number of samples in the training dataset.

* __train -> epochs__: The number of epochs is the number of complete passes through the training dataset.  The number of epochs can be set to an integer value between one and infinity.

* __train -> augment_multiplier__: You can use this setting to augment your training data. 1 means add 1x to the dataset (double it). 2 means add 2x (triple it).

Some other settings:

* __train -> max_negative_sampling_ratio__: Ratio of negative example sampling. Ratio = negative examples / positive examples
You can keep all the other setting to default.

* __test -> split_ratio__: This is a ratio for splitting a held-out test set from your dataset. The held-out test set will not be used for training. It will only be used when evaluating the model once training is completed. If value is 0.1 = 10% of dataset is split into held-out test set, and the model will be trained using remaining 90% of the data.

* __transforms__: Transform settings are used to define specific transformations for data augmentation. If the value for __augment_multiplier__ is greater than 0, you can modify the __transforms__ settings depending on how you want to augment your training dataset.

    To apply __RandomRotate__ and __RandomCrop__ transforms, you also need to set __p__ value to greater than 0.
p = probability between 0 and 1. If __p__ is 0 then that transform is not applied. If __p__ is 0.5 then half the original images get transformed. If it's 1 then all the original images get transformed.

Here is the default configuration for training a Selective Attention Network. 



``` yml
data:
  input_dim: 256

train:
  batch_size: 64
  epochs: 100
  max_negative_sampling_ratio: 0.3  # Ratio of negative example sampling. Ratio = negative examples / positive examples
  augment_multiplier: 0  # 1 means add 1x to the dataset (double it). 2 means add 2x (triple it).

test:
  split_ratio: 0.1


transforms:
  HorizontalFlip: False
  VerticalFlip: False
  Rotate:
    RandomRotate:
      p: 0
      rotate_min: -180
      rotate_max: 180
    Rotate90: False
  RandomCropScale: False
  ShiftScaleRotate: False
  RandomCrop:
    p: 0
    height: 118
    width: 118
  Noise: False
  Contrast: False
  Blur: False
  Distort: False
  Cutout:
    num_holes: 0
    hole_size: 25

optimizer:
  name: 'Adam'  # Choices: ['Adam']
  params:
    lr: 1.0e-3 # learning rate or step size.
```
