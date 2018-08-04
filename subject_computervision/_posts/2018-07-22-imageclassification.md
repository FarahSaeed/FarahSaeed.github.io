---
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      read_time: true
      comments: true
      share: true
      related: true
title:  "Image Classification"
date:   2018-07-22
permalink: /ComputerVision/
---

<style> 

.embed-container {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  max-width: 100%;
}

.embed-container iframe, .embed-container object, .embed-container embed {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}


.page__content {

font-size: 70%;
}
h4
{
font-size: 150%;
}
h5
{
font-size: 100%;
}
</style>

<div class="embed-container">
  <iframe
      width="640"
      height="480"
      src="https://drive.google.com/file/d/1IzALr7F8JBIUMTMUPOaftwQxJ1R7R3si/preview"
      frameborder="0"
      allowfullscreen=""
	  autoplay="1">
  </iframe>
</div>



Hi Guys, Hope you’re all doing great.

Above video shows Image Classification task accomplished using Convolutional Neural Network. In this post, I’ll be going through the entire process I have adopted to accomplish this task. 

#### Goal
The Goal is to classify images among the following 5 categories:
-  Indoor
-  Outdoor
-  Night
-  Day
-  Landscape

User is supposed to select a category to display all related images.

![](/assets/post_assets/2018-07-22-imageclassification_img1.jpg)

#### Dataset
For each of the 5 categories, I collected the images from Google Search. These are the number of images I collected, and labels for each category. The total dataset comprised around 8000 images.

|Class 		|Label 	|No of Images |
|:---------:|:-----:|:-----------:|
|Indoor 	|0		|2200         |
|Outdoor 	|1		|2476         |
|Night 		|2		|1143         |
|Day 		|3		|1689         |
|Landscape 	|4		|588          |


#### Transfer Learning
The classifier used is Convolutional Neural Network. I have used [VGG Places CNN](http://places.csail.mit.edu/downloadCNN.html) to extract features from Images. Here is the architecture of this Network.


|Layer			|Dimension			 |
|:--------------|:-------------------|
|Data (input)	|50,3,224,224        |
|conv1_1		|50,64,224,224       |
|conv1_2		|50,64,224,224       |
|pool1			|50,64,112,112       |
|conv2_1		|50,128,112,112      |
|conv2_2		|50,128,112,112      |
|pool2			|50,128,56,56        |
|conv3_1		|50,256,56,56        |
|conv3_2		|50,256,56,56        |
|conv3_3		|50,256,56,56        |
|pool3			|50,256,28,28        |
|conv4_1		|50,512,28,28        |
|conv4_2		|50,512,28,28        |
|conv4_3		|50,512,28,28        |
|pool4			|50,512,14,14        |
|conv5_1		|50,512,14,14        |
|conv5_2		|50,512,14,14        |
|conv5_3		|50,512,14,14        |
|pool5			|50,512,7,7          |
|fc6			|50,4096             |
|fc7			|50,4096             |


I have plugged a Softmax classifier as the last layer in the above network. This layer takes in fc7 Features  from the previous layer and outputs five probabilities corresponding each category.

##### Training
The last layer comprising Softmax Classifier is trained on 70% of the dataset. The remaining 30% is used for testing purpose. 
##### Testing
87.5% Images are correctly classified among the test set. Following is the confusion matrix for classifications on the test set.

![](/assets/post_assets/2018-07-22-imageclassification_img2.PNG)

To see how the classifier is performing on unseen data, here is a video showing the classification on unseen images neither part of test or train set.



<div class="embed-container">
  <iframe
      width="640"
      height="480"
      src="https://drive.google.com/file/d/17XXLWoamNV55NL21OH8fhpM9G8vOK5Q5/preview"
      frameborder="0"
      allowfullscreen=""
	  autoplay="1">
  </iframe>
</div>


