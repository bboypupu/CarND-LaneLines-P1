# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

 
---

### Reflection

#### The pipeline I used was based on the logistic and consisted of 6 steps:

(Original test images:)

<img src="./test_images/solidYellowCurve.jpg " width="200">
<img src="./test_images/solidYellowLeft.jpg" width="200">
<img src="./test_images/solidYellowCurve2.jpg" width="200">
<img src="./test_images/solidWhiteRight.jpg" width="200">
<img src="./test_images/whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images/solidWhiteCurve.jpg" width="200">

---

1.  Convert the input image into grayscale for feature extraction steps later.

<img src="./test_images_output/grayscale_solidYellowCurve.jpg" width="200">
<img src="./test_images_output/grayscale_solidYellowLeft.jpg" width="200">
<img src="./test_images_output/grayscale_solidYellowCurve2.jpg" width="200">
<img src="./test_images_output/grayscale_solidWhiteRight.jpg" width="200">
<img src="./test_images_output/grayscale_whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images_output/grayscale_solidWhiteCurve.jpg" width="200">

---

2.  Blur the grayscale image with Gaussian filter to eliminate the noise.

<img src="./test_images_output/gaussian_blur_solidYellowCurve.jpg" width="200">
<img src="./test_images_output/gaussian_blur_solidYellowLeft.jpg" width="200">
<img src="./test_images_output/gaussian_blur_solidYellowCurve2.jpg" width="200">
<img src="./test_images_output/gaussian_blur_solidWhiteRight.jpg" width="200">
<img src="./test_images_output/gaussian_blur_whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images_output/gaussian_blur_solidWhiteCurve.jpg" width="200">

---

3.  Use Canny edge detector to find the edges in the image where the gradient are large.

<img src="./test_images_output/canny_solidYellowCurve.jpg" width="200">
<img src="./test_images_output/canny_solidYellowLeft.jpg" width="200">
<img src="./test_images_output/canny_solidYellowCurve2.jpg" width="200">
<img src="./test_images_output/canny_solidWhiteRight.jpg" width="200">
<img src="./test_images_output/canny_whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images_output/canny_solidWhiteCurve.jpg" width="200">

---

4.  Mask the region of interest with a polygon.

<img src="./test_images_output/masked_solidYellowCurve.jpg" width="200">
<img src="./test_images_output/masked_solidYellowLeft.jpg" width="200">
<img src="./test_images_output/masked_solidYellowCurve2.jpg" width="200">
<img src="./test_images_output/masked_solidWhiteRight.jpg" width="200">
<img src="./test_images_output/masked_whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images_output/masked_solidWhiteCurve.jpg" width="200">

---

5.  With Hough transfer, we can find the lines within the edges. While our target is to find the left and right line of the lane, we can filter the lines with the slope of them. Then avarage the middle points and slopes of the lines we found after the filter, we got the left and right line we wanted. To make the result more smooth and also to prevent the situation of finding no solid line from the current image, I use 50% weight to modify the current result with the previous ones. 

<img src="./test_images_output/hough_lines_solidYellowCurve.jpg" width="200">
<img src="./test_images_output/hough_lines_solidYellowLeft.jpg" width="200">
<img src="./test_images_output/hough_lines_solidYellowCurve2.jpg" width="200">
<img src="./test_images_output/hough_lines_solidWhiteRight.jpg" width="200">
<img src="./test_images_output/hough_lines_whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images_output/hough_lines_solidWhiteCurve.jpg" width="200">

---

5.  For demonstrate the lane line we found, merge the lines and the original image together with weight, then we'll have a delicated image with two lines detected from the image.

<img src="./test_images_output/result_solidYellowCurve.jpg" width="200">
<img src="./test_images_output/result_solidYellowLeft.jpg" width="200">
<img src="./test_images_output/result_solidYellowCurve2.jpg" width="200">
<img src="./test_images_output/result_solidWhiteRight.jpg" width="200">
<img src="./test_images_output/result_whiteCarLaneSwitch.jpg" width="200">
<img src="./test_images_output/result_solidWhiteCurve.jpg" width="200">

---

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the line color blend in to the background (road) or too many noise. While we can see in the challenge part, the detection ability of my pipeline would be affected when the road color changes and the lines on both sides were not different from the background enough to have clear edges; and the shadow of the tree would also cause huge noise to the detection.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to make more contrast to the region of interest.
