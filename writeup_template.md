# **Finding Lane Lines on the Road** 

## Writeup

### **Finding Lane Lines on the Road**

---


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[gray]: ./test_images_output/1.gray_solidWhiteCurve.jpg "Grayscale"

---

### Reflection

### 1. Pipeline description

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a Gaussian filter to smooth the image in order to remove the noise. The result was input to the Canny edge detector algorithm which find the pixels in the image where the gradient is higher and outputs a black image with the detected high gradient pixels now representing the edges.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

![Gray](/test_images_output/1.gray_solidWhiteCurve.jpg)


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
