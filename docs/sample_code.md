# Face Detection on Static Image

<pre><code>
import dnn
import cv2 as cv

#By default Low resolution DNN for face detector will be loaded.
#To load the high resolution Face detector please comment the below lines.
#dnn.FaceDetector.set_param("resolution", dnn.RESOLUTION.HIGH)
detectum = dnn.FaceDetector()
THRESHOLD = 0.4 # Value between 0 and 1 for confidence score

im = cv.imread('../data/beatles.jpg')
_, bboxes = detectum.process_frame(im, THRESHOLD)

# Loop through list (if empty this will be skipped) and overlay green bboxes
for i in bboxes:
    cv.rectangle(im, (i[0], i[1]), (i[2], i[3]), (0, 255, 0), 3)

cv.imwrite('../data/beatles_output.jpg', im)
</code></pre>