# CGIAR Wheat Growth Stage Challenge by CGIAR
 
<p align="center">

  [![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)

  [![GitHub contributors](https://img.shields.io/github/contributors/rstak/CGIAR-Wheat-Growth-Stage-Challenge-by-CGIAR)](https://github.com/RsTaK/CGIAR-Wheat-Growth-Stage-Challenge-by-CGIAR/graphs/contributors/)
  [![GitHub license](https://img.shields.io/github/license/rstak/CGIAR-Wheat-Growth-Stage-Challenge-by-CGIAR)](https://github.com/RsTaK/CGIAR-Wheat-Growth-Stage-Challenge-by-CGIAR/blob/master/LICENSE)
</p>  

<img src="assets\header.jpg"/>

# About

[Picture-based insurance (PBI)](https://www.ifpri.org/project/PBInsurance) improves crop insurance for small scale farmers around the world, where images from a smartphone camera keep a record of a crop’s growth and record any damage events that will affect insurance payouts. PBI is a great way for insurers to verify events and to monitor crop growth, but it can also generate overwhelming amounts of data once images stream in from thousands of farmers.

Here, We will automate one part of the data processing pipeline: 
* Estimating the growth stage (from scale of 1 - 7)  of a wheat crop based on an image sent in by the farmer. 
* The images are automatically cropped to show a section of the field

<img src="assets\Wheat table.png"/>

Dataset provided by [CGIAR Platform for Big Data in Agriculture](https://bigdata.cgiar.org) via [Zindi Data Science Competition](https://zindi.africa).

Some of the labels have been determined by experts, and may be more reliable than the other labels which have been indicated by the farmers.

# Summary of Approach

Create an ensemble from a library of diverse models with different architectures and augmentations. All models are initially pre-trained on imagenet and fine-tuned on the dataset. 

<img src="assets\Wheat arc.png"/>

## Model Architectures

The following architecturs are included in the library of models:

* EfficientNet B2 : Image Size 224x224
* EfficientNet B3 : Image Size 224x224
* EfficientNet B3 : Image Size 256x256

# Data Augmentations

The following augmentations are included for EfficientNet B2 : Image Size 224x224 and EfficientNet B3 : Image Size 256x256

* Rotate
* RandomResizedCropGPU
* HorizontalFlip
* Normalize

The following augmentations are included for EfficientNet B3 : Image Size 224x224

* Rotate
* RandomResizedCrop
* Brightness
* Wrap
* Normalize

# Configuration

Leveraged the power of fastai library which uses one cycle training policy.

Trained for 70 epochs keeping the pre-trained encoder parameters frozen, and then for a further 40 epochs allowing the encoder weights to be updated.

# Dealing with Expert's vs Farmer's labels

I found out there were quite inaccurate labels provided by farmer. So, our solution only uses labels given by Experts.

# Ensemble 

Judged on the performance, EfficientNet B3 : Image Size 224x224 was given maximum weightage followed by EfficientNet B3 : Image Size 256x256.

With our solution, We have Root Mean Square Error (RSME) of 0.4087.

# License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/RsTaK/CGIAR-Wheat-Growth-Stage-Challenge-by-CGIAR/blob/master/LICENSE) file for details.
