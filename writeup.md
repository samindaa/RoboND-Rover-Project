## Project: Search and Sample Return
### Saminda Abeyruwan

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.

The notebook, _Rover Project Test Notebook_, provides a sandbox environment to get familiar with
the image processing, and transformations useful for the send part of the project. First, I have used
Udacity provided datasets to work with perspective transformation, and tune the color thresholds. 

Instead of working with the RGB color space, I have used the HSV color space - based on the experience
applying image processing methods presented in the self driving car course. Since, H is almost 
constant, I only have to work with S and V for tune color threshold. 

The empirical evidence has shown that only V channel is provide enough information to select
the navigable area.  

![alt text](./misc/img2_LV.png)

I have used a histogram to find the best threshold for calibration images _test_dataset_, and 
the function __ground_thresh_with_hsv__ provides the implementation. I have also analysed the 
profies on S and V for non-navigable areas while tuning the threshold. 

I have used both S and V channels to find rocks in __rock_thresh_with_hsv__, and a histogram analysis
directly provided the thresholds.  

![alt text](./misc/rock_threshed3.png)


#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 

As recommended by project video, I have created the _mask_ in __perspect_transform__, which has
been used in __process_image__ to generate the obstacle map. I have followed the instructions
therewith to implement the method and generated the video. 

<p align="center">
<img src="output/test_mapping.gif" width="500"/>
</p>

I have collected a training dataset, using the training mode in the simulator with setting __1024 x 768__, 
__Fastest__, and on a Mac. The parameter, __v_thresh=200__, for __ground_thresh_with_hsv__ worked 
well here as well as the autonomous mode. An example image, perspective transformation, rover coordinate,
and polar coordinate as follow.

![alt text](./misc/nav_train.png)

I have used the parameters, __s_thresh = 200, v_thresh_min = 100,__ and __v_thresh_max = 180__ to detect
rocks in test and training images. For example, on my training set -- __1024 x 768__, 
__Fastest__, and __Mac__ -- the image _robocam_2018_07_04_16_05_10_350.png_ and the threshold image 
as follows:

![alt text](./misc/rock_img_train.png)

![alt text](./misc/rock_img_th.png)
 

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  



![alt text][image3]


