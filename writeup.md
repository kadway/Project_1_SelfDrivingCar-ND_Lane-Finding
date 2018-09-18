# **Finding Lane Lines on the Road** 

## Writeup report

[//]: # (## **Finding Lane Lines on the Road**)

---


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (This may be the most platform independent comment)

[Final]: ./test_images_output/6.final_solidWhiteCurve.jpg "Identified lanes"

---

### Reflection

### 1. Pipeline description

My pipeline consisted 5 main steps: 
First, I converted the images to grayscale:
[Gray]: ./test_images_output/1.gray_solidWhiteCurve.jpg "Grayscale image"

I then applied a Gaussian filter to smooth the image in order to remove the noise:
[Gauss]: ./test_images_output/2.gauss_solidWhiteCurve.jpg "Gaussian smoothing"

The resulting image was then used as input to the Canny edge detector algorithm, which finds where in the image the pixels have the highest gradient. The output is a black image with the detected high gradient pixels now representing the edges.
[Canny]: ./test_images_output/3.canny_solidWhiteCurve.jpg "Canny edge detector"

With the the edges of the image detected, then a mask was applied.
It consisted of creating a polygon whose interior, when overlaped with the image with the detected edges, would define the relevant content to be further processed, meaning a delimitating of the image space where I know the lane lines would be.
[Masked Edges]: ./test_images_output/4.masked_edges_solidWhiteCurve.jpg "Masked edges"

Next step was to use the masked detected egdes as an input to the Hough Transform.
The Hough transform gives the x,y points of all the lines detected.
With the resulting list of points, it was necessary to decide which ones were relevant in order to draw the complete lines on the original image. In order to do so, I modified the draw_lines() function to calculate all of the line slopes in the list of line points, exclude the slopes close to zero and make an average with the selected slopes. The average slope was then used to compare which lines had a pre-determined allowed distance to the average. The lines which have a fitting slope to these criterias have then their x,y points saved in a list. Two lists of points were created, one for negative slope lines and one for positive slope. Also the minimum y values were saved.
With this data points separated by their positive or negative slope, it was then possible to extrapolate their best fitting line.
To find the lines, the cv2.fitLine function was used. It required as input the list of line points and the distribution type. The used distribution was the cv2.DIST_L2 which performs the least squares method.
The output of this funtion was (vx, vy) which was a normalized vector collinear to the line and (x0, y0) was a point on the line.
With vx and vy was posible to calculate the slope of the fitted line (vy/vx = m) and together with the (x0,y0) the intercept value was calculated ( b = y - m.x).
At this point the equation of the line (y = m.x + b) was known and could be used to find any coordinate of it.
The x points were calculated for the minimum y point found on the lines and for the edge of the image which was the highest y value.
The lines were then drawn:
[Hough]: ./test_images_output/5.hough_solidWhiteCurve.jpg "Hough drawn lines"

The lines were then applied to the original image:

![Final](/test_images_output/6.final_solidWhiteCurve.jpg)


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
