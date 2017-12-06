# Udacity-Self-Driving-Car-Traffic-Signs-Classifier-Project
My project pipeline for the Udacity Self-Driving-Car ND Project 2 - Traffic Sign Classifier

** Deep Learning **

**Project: Build a Traffic Sign Recognition Classifier**

The goal steps of this project are the following:
* Load the data set (see below for links to the project data set)

* Explore, summarize and visualize the data set

* Design, train and test a model architecture

* Use the model to make predictions on new images

* Analyze the softmax probabilities of the new images

* Summarize the results with a written report


## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! 

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is ? (34799, 32, 32, 3) 
* The size of the validation set is ? (4410, 32, 32, 3)
* The size of test set is ? (12630, 32, 32, 3) 
* The shape of a traffic sign image is ? (32, 32, 3) 
* The number of unique classes/labels in the data set is ? 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is histogram showing the frequency of the traffic sign classes in the training set.

![](images/frequency_of_classes_training_set.png)

The five most frequently met classes were:

ClassId	SignName
2	 Speed limit (50km/h)
1	 Speed limit (30km/h)
13 Yield
12 Priority road
38 Keep right

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

For the purposes of the project, I have decided to keep colour channels.

To address varying contrast I have performed Histogram Equalization using OpenCV (https://docs.opencv.org/3.1.0/d5/daf/tutorial_py_histogram_equalization.html). Please see Jupyter notebook for comparison of traffic sign images before and after histogram normalization.

As a last step, I normalized the image date to faciliate learning by the neural network.

I have decided to not to generate additional as this will be explored later outside project submission, dataset augmentation could be an additional tool which could deliver additional accuracy improvements on the test data. However, as I have achieved accuracy of the 

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

The model was motivate by LeNet architecture, however it was different in that I have used more filters in the first and second convolutional layers.This resulted in significantly better performance when compared with using original LeNet architecture. 

My final model consisted of the following layers:

|      Layer      |               Description                |
| :-------------: | :--------------------------------------: |
|      Input      |            32x32x3 RGB image             |
| Convolution 5x5 | x32,valid padding,outputs 28x28x32       |
|      RELU       |                                          |
|   Max pooling   |      2x2 stride,  outputs 14x14x32       |
| Convolution 5x5 | x64 stride,valid padding,outputs 10x10x16|
|      RELU       |                                          |
|   Max pooling   |      2x2 stride,  outputs 5x5x16         |
| Fully connected |         outputs 120                      |
|      RELU       |                                          |
|     dropout     |                                          |
| Fully connected |         outputs 84                       |
|      RELU       |                                          |
|     dropout     |                                          |
| Fully connected |         outputs # of classes             |


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used Adam optimizes and 0.001 learning rate. The batch size was 128 with 20 epochs. Additionally I have used Xaver initialization, dropout (keep_prob = 0.5) and L2 regularization on the weights. It has to be noted that both dropout and L2 regularization were used only on two fully connected layers - the convolutional layers use parameter sharing which is a form of regularization already. A

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 1.000
* validation set accuracy of 0.971
* test set accuracy of 0.957

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?

I have chosen LeNet to see how it performs on this particular dataset. Some improvements in termns of optmizer were made, allowing to obtaine validation accuracy over 97%. It is planned to develop this further outside the project to achieve 98%-99% accuracy rate.

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![](images/german_signs.png)

I have taken first 5 signs (4 from the top row and 1 one on the left from the bottom row).

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

|     Image                              |  Prediction             |
| :-------------------------------------:| :----------------------:|
|   Speed limit - 60km/h                 |   Speed limit - 60km/h  |
|   Turn left ahead                      |  Turn left ahead        |
|   Speed limit - 60km/h                 |   Speed limit - 60km/h  |
|   Priority Road                        |   Prioirity Road        |
|   Keep right                           |   Keep right            |


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. This is in line with accuracy on the test set of 95.7%


#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located at the end of the Ipython notebook.

For all the images, the model is quite sure about the classes. In all cases the top class probability was in excess of 0.98-0.99. See Jupyter notebook for more details.
