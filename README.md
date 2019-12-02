# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image2]: ./test_images_output/blur.jpg "Grayscale"
[image3]: ./test_images_output/masked.jpg "Edges in the Region of Interest"
[image4]: ./test_images_output/lines.jpg "Lines after Hough Transform"
[image5]: ./test_images_output/final.jpg "Resulting Image"


---

This project was submitted for the Udacity Self-Driving Car Nanodegree program. 
In this project I summarize my pipeline for detecting highway lane lines on a video stream using OpenCV image analysis techniques to identify lines, including Hough Transforms and Canny Edge detection.

<video width="320" height="240" controls>
  <source src="./test_videos_output/solidWhiteRight.mp4.mov" type="video/mp4">
</video>

### 1. Pipeline description

My pipeline consists of 5 steps. First of all, convert the images to grayscale and apply gaussian blur to smooth the image as shown bellow.  

![alt text][image2]

Use the Canny algorithm, a famous and widespread edge detection algorithm to detect the edges of the image. 
Define a quadrangular binary mask and apply it to the image to make only the region of interest visible. 

![alt text][image3]

Finally, to identify lines in the edge image, use Hough transform which extracts features from the image space to the so called Hough space. That means that a line y = mx+b in the image space corresponds to a point in the Hough space. The following figure shows the resulting fitted lines after performing Hough transform.     

![alt text][image4]

In order to draw a single line on the left and right lanes, modify the draw_lines() function by calculating the slope of each line segment. After that, fit a line function of the line seqments for each lane to get the coefficients of the resulting line. Assuming that the line is always in the ROI (region of interest), calculate the x-values of the vertices by setting the y-values to the bottom/top values of ROI. By using an moving average technique on the coefficients try to stabilize the line. Furthermore, adjust some slope range to filter out bad line segments.  

![alt text][image5]

### 2. Potential shortcomings

One potential shortcoming would be what would happen when an another vehicle is crossing the lane lines or if there is more traffic (more vehicles) on the road. Furthermore, what would happen when my car is crossing the lane line. 

What would happen with different weather and light conditions. 

A further shortcoming could be if the lane lines are not visible.

Another shortcoming could be if the road is more curved.  

### 3. Possible improvements

A possible improvement would be to use Kalman filter for better estimation and stabilization. 

Another potential improvement could be to use more color spaces for better detection under different conditions. 








