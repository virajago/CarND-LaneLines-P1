#**Finding Lane Lines on the Road**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I applied Gaussian Blur with kernel size of 5 and finally ran it through Canny edge detection. I played with different parameters for Canny and finally settled on the 50 and 150 for low and high thresholds respectively. Once the edges are detected, I applied a mask to retain only the edges which are of interest. This step is done before drawing lines in order to avoid lines which are not of interest and which can skew the calculation later on.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as follows
* The intuition is that lane lines are much clearer and visible at the bottom of the image than at the top.
* First I select only the edges in the bottom half of the image to draw lines
* then calculate the slope and intercept of the lines to be drawn
* if the slope is negative then it is a left line else if the slope is positive it is a right lane
* for both left and right lanes classify the scope and intercept into 2 groups viz lines which start at the bottom edge of the image and all other lines.
* we will draw lines from bottom of the image to y = 325 which is arrived at by looking at the image.
* if we found lines starting at the bottom of the image then we use the average slope and average intercept of those lines to calculate the x coordinates
* finally draw both the left and right lanes
If you'd like to include images to show how the pipeline works, here is how to include an image:

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


The current solution looks for lines at the bottom of the image and then uses the slope of those lines to extrapolate and draw the lane lines. The lines are a bit unstable when detected on a video. Also the solution fails when the lanes lines are curved

###3. Suggest possible improvements to your pipeline

Apply stabilization to lane lines by remembering the lines detected in previous frames and then averaging the slope with the current frame before drawing the new line.
