# Free tools for developers

**Checkout this Github Repository for the most updated versions:**
[https://github.com/XailientPublic/free_tools](https://github.com/XailientPublic/free_tools)


## Split a video into frames for training data

File: [video_2_frames.py](https://github.com/XailientPublic/free_tools/blob/master/video_2_frames.py)

This tool allows developers to quickly split a video into frames,
with the aim in create training data for model production.

This python script allows developers to either:

1. Go through each frame and manually save the frames you want (default).

`$ python3 video_2_frames <path_to_video>`

2. Save every ith frame in the video.

`$ python3 video_2_frames --every <integer> <path_to_video>`


## Converion of different annotation formats

File: [convert.py](https://github.com/XailientPublic/free_tools/blob/master/convert.py)

A script to convert different annotations formats to the format required by the Xailient Console.

Currently supported formats for this conversion script are pascalvoc/labelimg, labelme, coco, and yolo formats.

Choices for input_format argument are 'voc', 'coco', 'labelme', 'yolo'

- For annotations present in a single file (e.g. COCO), input_path represents the path to the JSON file. 

- While for separate annotations for each image (e.g. Pascal VOC, yolo, labelme), input_path represents
the path to the folder where the annotations reside.

The output_path is the path and name of the converted xailient annotations.

Examples of usage:

`$ python3 convert.py --input_path example/coco_annotations.json --input_format coco --output_path example/xailient_labels.csv`

<br>
<br>
<br>
<br>
