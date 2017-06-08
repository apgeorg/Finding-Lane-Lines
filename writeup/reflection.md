# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image2]: ../test_images_output/blur.jpg "Grayscale"
[image3]: ../test_images_output/masked.jpg "Edges in the Region of Interest"
[image4]: ../test_images_output/lines.jpg "Lines after Hough Transform"
[image5]: ../test_images_output/final.jpg "Resulting Image"

---

## Reflection

### 1. Pipeline description

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian blur to smooth the image as shown bellow.  

![alt text][image2]

After that, I use the Canny algorithm, an famous and widespread edge detection algorithm to detect the edges of the image. 
Further, I defined a quadrangular binary mask and apply it to the image to make only the region of interest visible. 

![alt text][image3]

Finally, to identify lines in the edge image, I use Hough transform which extracts features from the image space to the so called Hough space. That means that a line y = mx+b in the image space corresponds to a point in the Hough space. The following figure shows the resulting fitted lines after performing Hough transform.     

![alt text][image4]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the slope of each line segment. After that I fit a line function of the line seqments for each lane to get the coefficients of the resulting line. Assuming that the line is always in the ROI (region of interest), I could calculate the x-values of the vertices by setting the y-values to the bottom/top values of ROI. By using an moving average technique on the coefficients I was trying to stabilize the line. Furthermore I adjust some slope range to filter out bad line segments.  

![alt text][image5]

### 2. Potential shortcomings

One potential shortcoming would be what would happen when an another vehicle is crossing the lane lines or if there is more traffic (more vehicles) on the road. Furthermore, what would happen when my car is crossing the lane line. 

What would happen with different weather and light conditions. 

A further shortcoming could be if the lane lines are not visible.

Another shortcoming could be if the road is more curved.  

### 3. Possible improvements

A possible improvement would be to use Kalman filter for better estimation and stabilization. 

Another potential improvement could be to use more color spaces for better detection under different conditions. 
