#  **Behavioral Cloning** 

## Udacity Self-Driving Car Nanodegree Project 4



**The goals / steps of this project are the following:**

* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/placeholder.png "Model Visualization"
[image2]: ./examples/placeholder.png "Grayscaling"
[image3]: ./examples/placeholder_small.png "Recovery Image"
[image4]: ./examples/placeholder_small.png "Recovery Image"
[image5]: ./examples/placeholder_small.png "Recovery Image"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image"
[image10]: ./examples/csv_header.png "csv header Image"


---
### Files Submitted & Code Quality

#### 1. Submission includes all required files as below:

File Name | Description
----------|-----------
model.py |all folder path varialbes applied for udacity workspace
model.h5 |              generated from workspace and works for track one in simulator
writeup_report.md |      summarizing the results and the same contents as README.MD
drive.py        |       for driving the car in autonomous mode, original file provided by Udacity
video.mp4 |  video under autonomous mode on track one

Additional files

File Name | Description
----------|-----------
model.ipynb | all folder path varialbles applied for my local drive
model.html |  file exported from Jupytor Notebook with result from model.ipynb 
model_local_track1.h5 | generated from my laptop and was not compatible with simulator on workspace

At begining I ran the code successfuly at my laptop to save the data to h5 file which unfornately was not compatible with the simulator on workplace. I thought it was due to different versions of keras and I tried to downgrade keras from 2.3.1 to version 2.2.4 on my laptop and generated the model.h5 again, but it still didnot work. 

Later, I found out it seems like other students also encountered such problem and someone suggested to run the code on workspace and it did work for me too.

#### 2. Submission includes functional code

The car can be driven autonomously around the track One by executing 
```sh
python drive.py model.h5
```

#### 3. Remove header of csv file

There is a line of header in the file of "driving_log.csv" which should be removed from the list created from csv file.
![alt text][image10]

After appending all lines into the list, the first line (header in csv file) was pop out of the list, otherwise it will created problem during reading images.

```sh
lines=[]
with open("../p4_data/data/driving_log.csv") as csvfile:
    reader=csv.reader(csvfile)
    for line in reader:
        lines.append(line)

lines.pop(0)
```

#### 4. RGB format of image

The class material mentioned about the OpenCV read images file into BGR formet, instread of using OpenCV and convert to RGB format, I used the mpimg funciton from matplotlib.  I remember that we have to deal with similar problem when I was working on the first two projects of lane finding. 

```sh
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
...
...
                    name = '../p4_data/data/IMG/'+batch_sample[i].split('/')[-1]
                    image = mpimg.imread(name)
                    angle = float(batch_sample[3])
```




**_I was spending lots of time debugging and later I realized lot of time was spent on these 3 issues below_**

* Run the model.py under workspace to generate model.h5 to make sure it work with simulator
* Remove the header from csv file 
* Make sure the images read into RGB format


### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 3x3 filter sizes and depths between 32 and 128 (model.py lines 18-24) 

The model includes RELU layers to introduce nonlinearity (code line 20), and the data is normalized in the model using a Keras lambda layer (code line 18). 

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting (model.py lines 21). 

The model was trained and validated on different data sets to ensure that the model was not overfitting (code line 10-16). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 25).

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road ... 

For details about how I created the training data, see the next section. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the ... I thought this model might be appropriate because ...

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I modified the model so that ...

Then I ... 

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track... to improve the driving behavior in these cases, I ....

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...

Here is a visualization of the architecture (note: visualizing the architecture is optional according to the project rubric)

![alt text][image1]

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to .... These images show what a recovery looks like starting from ... :

![alt text][image3]
![alt text][image4]
![alt text][image5]

Then I repeated this process on track two in order to get more data points.

To augment the data sat, I also flipped images and angles thinking that this would ... For example, here is an image that has then been flipped:

![alt text][image6]
![alt text][image7]

Etc ....

After the collection process, I had X number of data points. I then preprocessed this data by ...


I finally randomly shuffled the data set and put Y% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was Z as evidenced by ... I used an adam optimizer so that manually training the learning rate wasn't necessary.
