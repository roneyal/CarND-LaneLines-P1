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

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied the gaussian blur filter.
I ran the Canny edge detection algorithm on the blurred image and then filtered only region of interest which is bounded by a trapezoid.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by segmenting the lines to two groups according to their slope.
Lines with negative slope were segmented to the left group and lines with positive slope were assigned to the right group. Lines with a slope with magnitude less than 0.1 were dropped to avoid noisy classification.

Within each group I averaged the slope and the center point and extrapolated to the extent of the region of interest to create a full line. The averaging was done in a weighted manner - each line in the image was weighted according to its length and closeness to the camera.

Here is an example output:

![ex_img][./test_images/out/solidWhiteCurve_lanes.jpg]

###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the vehicle is not in the center of the lane, causing the region of interest to shift.

Another shortcoming could be if the vehicle orientation is off course and then the thresholds for the angles would be incorrect.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to use a more sophisticated clustering algorithm for separating the lines to two groups instead of hard thresholds.

Another potential improvement could be to deal better with curved lanes by fitting a higher polynomial curve to the lane borders.
