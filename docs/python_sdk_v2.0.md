# Xailient SDK API Documentation

**Xailient SDK Version: 2.0**

## roi_bbox.ROIBBoxModel Class

``` python
detectum = roi_bbox.ROIBBoxModel()
```

#### Arguments

| Arguments     | Input Type    | Default Value | Description   |
| ------------- |:-------------:| :------------:| -------------|
| threads _(optional)_         | int           | 1             |   Number of threads to start for running the Detector. This gives the ability to run multiple threads for inferencing. This value should be tuned and select based on the use case to maximise overall performance. |

#### Example

1. Using 2 threads

    For example, your device has 4 cores and each core runs 1 process thread. If you want 1 thread to be running dedicatedly for camera inputs, one thread for post processing, then you can reserve two threads for the Detector so that it will perform efficiently.

    This is how you would initialize the Detector so that it uses two cores:

    ``` python
    detectum = roi_bbox.ROIBBoxModel(2)
    ```

2. Using 1 thread

    ``` python
    detectum = roi_bbox.ROIBBoxModel()
    ```

    or 

    ``` python
    detectum = roi_bbox.ROIBBoxModel(1)
    ```

3. Using 4 threads

    ``` python
    detectum = roi_bbox.ROIBBoxModel(4)
    ```

### options().set_option Method

```python
detectum.options().set_option('OPTION', 'VALUE')
```

You can use options().set_option() method to set the following settings:

| Setting     | Option    | Value | Description   |
| ------------- |:-------------:| :------------:| -------------|
| Set bounding box threshold         | dnn_threshold           | float             |   Value between 0 and 1 for confidence score |
| Enable samping the images         | sampling_frequency           | int             |   Enable this to cause the SDK to send every n<sup>th</sup> detection to the cloud where the sampled images can be used for retraining newer and more accurate models. |

#### Arguments

| Arguments     | Input Type    |
| ------------- |:-------------:|
| OPTION         | string           |
| VALUE         | int/string        |

#### Example

1. Set bounding box threshold

    ``` python
    detectum.options().set_option('dnn_threshold', 0.5)
    ```

2. Enable samping the images

    Enable this to cause the SDK to send every 1000th detection to the cloud where the sampled images can be used for retraining newer and more accurate models.

    ``` python
    detectum.options().set_option('sampling_frequency', 1000)
    ```

### process_image Method

``` python
bboxes = detectum.process_image(numpy.ndarray)
```

#### Arguments

| Arguments     | Input Type    | Default Value | Description   |
| ------------- |:-------------:| :------------:| -------------|
| image         | numpy.ndarray           | -             |   Image as numpy array |

#### Returns

| Returns     | Type    |  Description   |
| ------------- |:-------------:| :------------:| 
| _         |    -        |        -      |
| bboxes         |    list      | Each item (bbox) in the list is a dictionary of bounding box coordinates, where bbox.xmin = xmin, bbox.ymin = ymin, bbox.xmax = xmax, bbox.ymax = ymax |

#### Example - Using OpenCV to read image

``` python
import os
from xailient import roi_bbox
import cv2 as cv

detectum = roi_bbox.ROIBBoxModel()

data_dir = os.path.join(os.path.dirname(__file__), '..', 'data')
im = cv.imread(os.path.join(data_dir, 'beatles.jpg'))
# opencv reads BGR format so we have to convert this to RGB
im = cv2.cvtColor(im, cv2.COLOR_BGR2RGB)

bboxes = detectum.process_image(im)

# Loop through list (if empty this will be skipped) and overlay green bboxes
# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
for bbox in bboxes:
    pt1 = (bbox.xmin, bbox.ymin)
    pt2 = (bbox.xmax, bbox.ymax)
    cv.rectangle(im, pt1, pt2, (0, 255, 0))

# convert it back to RGB
im = cv.cvtColor(im, cv.COLOR_RGB2BGR)
cv.imwrite('beatles_output.jpg', im)
```

#### Example -  Using skimage to read image

``` python
import os
from xailient import roi_bbox
import skimage.io

detectum = roi_bbox.ROIBBoxModel()

data_dir = os.path.join(os.path.dirname(__file__), '..', 'data')
im = skimage.io.imread(os.path.join(data_dir, 'beatles.jpg'))
bboxes = detectum.process_image(im)

# Loop through list (if empty this will be skipped) and overlay green bboxes
# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
for bbox in bboxes:
    pt1 = (bbox.xmin, bbox.ymin)
    pt2 = (bbox.xmax, bbox.ymax)
    cv.rectangle(im, pt1, pt2, (0, 255, 0))

skimage.io.imsave('beatles_output.jpg', im)
```
