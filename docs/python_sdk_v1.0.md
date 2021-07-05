# Xailient SDK API Documentation

**Xailient SDK Version: 1.0.x**

## dnn.Detector Class

``` python
detector = dnn.Detector(int)
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
    detector = dnn.Detector(2)
    ```

2. Using 1 thread

    ``` python
    detector = dnn.Detector()
    ```

    or 

    ``` python
    detector = dnn.Detector(1)
    ```

3. Using 4 threads

    ``` python
    detector = dnn.Detector(4)
    ```

### process_frame Method

``` python
_, bboxes = detector.process_frame(numpy.ndarray, float)
```

#### Arguments

| Arguments     | Input Type    | Default Value | Description   |
| ------------- |:-------------:| :------------:| -------------|
| image         | numpy.ndarray           | -             |   Image as numpy array |
| threshold _(optional)_         | float           | The default threshold is built into the SDK and is an optimal value determined when the model was trained.             |   Value between 0 and 1 for confidence score |

#### Returns

| Returns     | Type    |  Description   |
| ------------- |:-------------:| :------------:| 
| _         |    -        |        -      |
| bboxes         |    list      | Each item (bbox) in the list is a list of bounding box coordinates, where bbox[0] = xmin, bbox[1] = ymin, bbox[2] = xmax, bbox[3] = ymax |

#### Example

``` python
from xailient import dnn
import cv2 as cv

detector = dnn.Detector()
THRESHOLD = 0.4

im = cv.imread('../data/beatles.jpg')

_, bboxes = detector.process_frame(im, THRESHOLD)

# Loop through list (if empty this will be skipped) and overlay green bboxes
# Format of bboxes is: xmin, ymin (top left), xmax, ymax (bottom right)
for bbox in bboxes:
    cv.rectangle(im, (bbox[0], bbox[1]), (bbox[2], bbox[3]), (0, 255, 0), 3)

cv.imwrite('../data/beatles_output.jpg', im)
```