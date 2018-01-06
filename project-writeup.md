# **Finding Lane Lines on the Road** 

## Writeup 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

I implemented the pipeline in the `process_image` function. It does the following things - 
* Coverts the image to grayscale
* Smooths the image using Guassian Blur to reduce the spikes in the image's color transitions
* Creates a trapezoidal region of interest by using a buffer to create an offset from the bottom and off the center. 
* Calculates hough lines with a set of parameters
* Overlays an extrapolated set of lane lines on the final image

In order to draw a single line on the left and right lanes, I modified the `draw_lines`()` function by ...
* Ignoring where slopes are too close to horizontal line (defined by absolute slope of less than 0.3)
* Tracking the the begin, end of every hough line and extracting the highest relevant number to figure out where to start the line and end the line. 
* Extrapolating the line to the bottom of the image by taking the slope and calculating the bottommost line. Used the medin of all slopes if for some reason the hough lines were straight or just a point. 
* Ultimately, drawing exactly two lines per image - one for left and one for right

Overall, this gets me reasonable results in most siutations like so - 
![alt text][whiteCarLaneSwitch.jpg
]

However plenty of other cases where it seems I need to tweak the parameters much more :( Like below - 

![alt text][solidWhiteRight.jpg
.jpg
]



### 2. Identify potential shortcomings with your current pipeline

Due to being behind and a bit short on time, didn't get a chance to play with the hough parameters too much. I tried a few variations but at some point I felt like my changes were counter acting each other and I was blindly fidling. I need to better build a system of understanding the changes to make more intelligent changes. 

### 3. Suggest possible improvements to your pipeline

Just like how there is a bottom extrapolation I do... I should do a top extrapolation as well. The two lines should never intersect. 

Need to review [this discussion](https://discussions.udacity.com/t/have-trouble-in-improve-draw-line-function/398760/11) thread to impove further on the hough parameters. 
