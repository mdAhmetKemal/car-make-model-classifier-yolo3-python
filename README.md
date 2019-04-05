# Car Make and Model classification example with YOLOv3 object detector

[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

## Introduction

A Python example for using [Spectrico's car make and model classifier](http://spectrico.com/car-make-model-recognition.html). It consists of object detector for finding the cars, and a classifier to recognize the makes and models of the detected cars. The object detector is an implementation of YOLOv3 (OpenCV DNN backend). It doesn't use GPU and one frame takes 1s to process on Intel Core i5-7600 CPU. YOLOv3 weights were downloaded from [YOLO website](http://pjreddie.com/darknet/yolo/). The classifier is based on Mobilenet v2 (TensorFlow backend). It takes 35 milliseconds on Intel Core i5-7600 CPU for single classification. It can be accelerated more by running on GPU and using batching. The light version of the classifier is slightly less accuracy but is 4 times faster. It is optimized for speed and is recommended for edge devices.

---
## Object Detection and Classification in images
This example takes an image as input, detects the cars using YOLOv3 object detector, crops the car images, makes them square while keeping the aspect ratio, resizes them to the input size of the classifier, and recognizes the make and model of each car. The result is shown on the display and saved as output.jpg image file.


#### Usage
Use --help to see usage of car_make_model_classifier_yolo3.py:
```
$ python car_make_model_classifier_yolo3.py --image cars.jpg
```
```
$ python car_make_model_classifier_yolo3.py [-h] [--yolo MODEL_PATH] [--confidence CONFIDENCE] [--threshold THRESHOLD] [--image]

required arguments:
  -i, --image              path to input image

optional arguments:
  -h, --help               show this help message and exit
  -y, --yolo MODEL_PATH    path to YOLO model weight file, default yolo-coco
  --confidence CONFIDENCE  minimum probability to filter weak detections, default 0.5
  --threshold THRESHOLD    threshold when applying non-maxima suppression, default 0.3
```
![image](https://github.com/spectrico/car-make-model-classifier-yolo3-python/blob/master/citroen-xantia-output.jpg?raw=true)

---
## Object Detection and Classification in video files
This example takes a video file as input, detects the cars in each frame using YOLOv3 object detector, crops the car images, makes them square while keeping the aspect ratio, resizes them to the input size of the classifier, and recognizes the make and model of each car. The result is saved as an output video file.


#### Usage
Use --help to see usage of car_make_model_classifier_yolo3_video.py:
```
$ python car_make_model_classifier_yolo3_video.py --input video.avi --output output.avi
```
```
$ python car_make_model_classifier_yolo3_video.py [-h] [--yolo MODEL_PATH] [--confidence CONFIDENCE] [--threshold THRESHOLD] [--input] [--output]

required arguments:
  -i, --input              path to input video
  -o, --output             path to output video

optional arguments:
  -h, --help               show this help message and exit
  --yolo MODEL_PATH        path to YOLO model weight file, default yolo-coco
  --confidence CONFIDENCE  minimum probability to filter weak detections, default 0.5
  --threshold THRESHOLD    threshold when applying non-maxima suppression, default 0.3
```
![image](https://github.com/spectrico/car-make-model-classifier-yolo3-python/blob/master/car_make_model_recognition.gif?raw=true)

---
## Requirements
  - python
  - numpy
  - tensorflow
  - opencv

---
## Configuration

The settings are stored in python file named config.py:
```
model_file = "model-weights-spectrico-mmr-mobilenet-128x128-344FF72B.pb"
label_file = "labels.txt"
input_layer = "input_1"
output_layer = "softmax/Softmax"
classifier_input_size = (128, 128)
```
***model_file*** is the path to the car make and model classifier
***classifier_input_size*** is the input size of the classifier
***label_file*** is the path to the text file, containing a list with the supported makes and models

---
## Credits
The examples are based on the tutorial by Adrian Rosebrock: [YOLO object detection with OpenCV](https://www.pyimagesearch.com/2018/11/12/yolo-object-detection-with-opencv/)
The YOLOv3 object detector is from: [YOLO: Real-Time Object Detection](http://pjreddie.com/darknet/yolo/)

```
@article{yolov3,
  title={YOLOv3: An Incremental Improvement},
  author={Redmon, Joseph and Farhadi, Ali},
  journal = {arXiv},
  year={2018}
}
```
The make and model classifier is based on MobileNetV2 mobile architecture: [MobileNetV2: Inverted Residuals and Linear Bottlenecks](https://arxiv.org/abs/1801.04381)

