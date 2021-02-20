# Car Plate Detector and Reading Plate Number

## Introduction
*In a modern world with images all around. It's a Computer Vision challenge to read text from images. One such realtime problem could be detecting and reading car plate numbers.*

## Problem Statement:
Aim is to detect car plate numbers from images. This problem can be be split into two parts:
1. Detecting car plates from images.
2. Extrating text from detected images.

## Data: 
Data was collected from Kaggle, linked it [here](https://www.kaggle.com/andrewmvd/car-plate-detection). \n
This dataset contains 433 images with bounding box annotations of the car license plates within the image.
Annotations are provided in the PASCAL VOC format. \n
Model for object detection is linked [here](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md).

## Project Architecture:
Following is the architecture we followed:
![Project Architecture](https://github.com/SanjaPanda/car-plate-detector/blob/main/images/Architechture.PNG)

## Data Wrangling:
In this step prepared the files for transfer learning of model:

1. Create a directory with appropriate folders as per requirement. And load it on Google Drive.
2. Create label_map.pbtxt file.
3. Create XML to CSV files for both train and test dataset. These files would be used to create TFRecords.
4. Unpack zip file and create a copy of pipeline.config in new model folder. Model used is 'SSD MobileNet V2 FPNLite 640x640'.
5. Edit pipeline.config file.

## Tranfer Learning and Model Training:
In this step trained the model to detect lisence plate number:

1. Install basic packages and libraries. object-detection-api, was also installed.
2. Generate TFRecords
3. Train Model
4. Export Model 


## Car Plate Number Extraction
Steps to extract plate number from images:

. Detected car plates, with a threshold of 0.6

. Cropped images based on thershold.

. Cleaned the images, converted image to gray scale. Resized image and smoothened it.

. Used OCRopus and performed binning on the image. Didn't use segmentation as the letters were getting converted in the middle hence would have hindered detection.

. This binned image was used to extract text from image using pyTesseract. OCRopus was throwing error due to too much segments in the image.

. Once the string was extracted, performmed preprocessing on the same to extract alpha-numeric charecters.

## Evaluation
. Object Detection evaluation:
	mAP: 0.493867
	mAR: 0.549057
. Evaluation of text recognition:
![Evaluation](https://github.com/SanjaPanda/car-plate-detector/blob/main/images/Recog_Eval.PNG)


## Solution

![Solution](https://github.com/SanjaPanda/car-plate-detector/blob/main/images/Cars386.png)
![Solution](https://github.com/SanjaPanda/car-plate-detector/blob/main/images/Cars428.png)

## Observations
Below are few observations:

. The threshold is set higher ie. 0.6 because even if plates are detected. Because with lower threshold, images detected are highly pixalated.
. Some charecters are getting jumbled eg. '8' and 'B'.
. Many a times images within the plates, don't help getting results.
. Adding rules to preprocessing extracted images.

## Resources
. Object Detection on Google Colab: https://medium.com/swlh/tensorflow-2-object-detection-api-with-google-colab-b2af171e81cc

. Step by Step Guide to Object Detection: https://www.dlology.com/blog/how-to-train-an-object-detection-model-easy-for-free/

. Car Plate Number Recogniser: https://github.com/theAIGuysCode/yolov4-custom-functions

. Extracting Text using OCRopus: https://www.danvk.org/2015/01/09/extracting-text-from-an-image-using-ocropus.html
