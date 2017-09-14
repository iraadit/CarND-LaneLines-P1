# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image0]: ./writeup_images/0_yellow_white.png "Yellow and White"
[image1]: ./writeup_images/1_gray.png "Grayscale"
[image2]: ./writeup_images/2_blur.png "Blur"
[image3]: ./writeup_images/3_canny.png "Canny"
[image4]: ./writeup_images/4_mask.png "Mask"
[image5]: ./writeup_images/5.1_hough.png "Hough"
[image6]: ./writeup_images/5.2_hough_single.png "Straight Hough"
[image7]: ./writeup_images/6.1_result.png "Result"
[image8]: ./writeup_images/6.2_result_single.png "Result Hough"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps :
1. Selecting yellow and white (corresponding to lanes) in images, by using HSL color space (to avoid shadows changing colors and patterns on road that could be interpreted as lines)
2. Converting the images to grayscale
3. Applying a gaussian blur to the images
4. Applying a canny edge detection to the images
5. Masking the images so that only the region of interest is kept
6. Processing the images with a Hough transform to identify lines
7. Finding the straight left and right single lines from all the lines obtained (as explained below)
8. Plotting the lines on the initial images
9. Showing result images
10. Saving result images (or videos) on hard drive

![alt text][image0]
![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]
![alt text][image8]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
1. Separating the left and right lines based on their slope
2. Deleting the outliers lines (slope too different from mean left and right slope, and then considered as not lane lines)
3. Calculating the average left and right slopes
4. Finding the intersection of the lines with the bottom of the image
4. Extrapolating the left and right straight lines based on the slopes and intersection, from bottom of screen to (chosen) « horizon »
5. [if movie] Calculating a moving average of the last positions of the straight lines, to smooth the result in time


Optional Challenge has also been done.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when 
1. The road is turning, and the lane lines aren’t lines anymore but curves
2. Going uphill or downhill, and so having the horizon being down or up in the image
4. Horizontal demarcation or intersections lines are found on the road
5. Lane lines aren’t white or yellow
6. Car is changing lane


### 3. Suggest possible improvements to your pipeline

Some possible improvements would be to
1. Fit the curves created by the lane (and not simply fit a line)
2. Automatically finding the horizon in the images (for cases when we are going up or down hill), so that we can dynamically adapt the region of interest and to where to extrapolate the straight lines
4. Cleaner code, in particular by creating functions to call
5. Find better values for the parameters of hough, canny,…

