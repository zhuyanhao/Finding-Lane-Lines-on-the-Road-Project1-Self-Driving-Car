# **Finding Lane Lines on the Road** 

## Udacity Self-Driving Car Engieer Nano Degree Project1
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
  Buidl a lane dector in Python with OpenCV. Canny edge detector, Guassian smoothing and Hough line transform and other techniques learned from Lesson1 are used to find lane lines in the test images/videos.
* Reflect on your work in a written report
  Shortcomings are listed with future improvements discussed.

Files contained in this repository:
  ./test_images - Original images for testing
  ./test_images_output - Images with lane lines 
  ./test_videos - Origianl videos for testing
  ./test_videos_output - Videos with lane lines
  
---

**Quick Example**

Original Image:
![](./test_images/solidWhiteCurve.jpg)
Image with Lanes:
![](./test_images_output/solidWhiteCurve.jpg)

---

### Reflection

### 1. Pipeline of Project
* Read in an image and convert it to grayscale
* Apply Gaussian smoothing to the grayscaled image
* Use canny edge detector to find all edges
* Define the region of interest(quadrilateral) and apply region masking
* Apply hough transformation to find the lines in the region of interest
* Draw the lines over the original image. More than one lines are generated from the previous step for left/right lane. We use the slope to detect if a specific line belongs to the left/right lane. Then we fit a liear polynomial among all the points and use that line as the left/right lane. It helps to reduce the number of lines in the image.
* For a video clip, we apply the above procedure to each frame.

### 2. Potential Shortcomings

* One shortcoming is that in the video testing, the lane lines could disappear in a specific frame. 
* The lane line direction is not always correct when the actual lane in is not that clear.
* It doesn't work well when the lane is not straight.

### 3. Suggest possible improvements to your pipeline

* Since the camera is fixed on the car, the angle of lane line could only take certain values. Thus, mathematical constraints can be added to limit the slope of lanes, which helps when the lane is not visible in the image.
* When car is driving on the road, the angle of lanes would never undergo a rapid change (unless in an accidient). Therefore, the lane in the previous frame can be used as an estimation of the next frame. When the lanes cannot be detected in the current frame, simply use the lanes from the previous frame.
* A new algorithm is needed to detect curved lanes.
