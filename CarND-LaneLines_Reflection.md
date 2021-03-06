# **Finding Lane Lines on the Road** 

## Reflection Write-up

---

**Finding Lane Lines on the Road**

The goals / steps of this project were the following:
* Build an image analysis pipeline that finds lane lines on the road
* Reflect on the work in a written report


[//]: # (Image References)

[image001]: ./images_output/image001.png "image001"
[fail001]: ./images_output/challenge_curved_lines_fail_001.PNG "fail001"

---

### Reflection

### 1. Pipeline description

The pipeline included 5 steps and modification of the draw_lines() function, the pipeline inculded:

Convert to grayscale and apply Gaussian Blur

Apply Canny transformation

Define a region of interest

Define a Hough lines transformation (utlizing the draw_lines() function)

Overlay (annotate) images with superimposed lines

![alt text][image001]

Within the hough_lines() function, draw_lines() function was used, which drew lines on the right and left of the lanes. This required found lines to be sorted into right and left lists, based on their slope (negative or positive respecitvley). The mean was then computed for the slopes and x,y points of the lines. From this information, the annotation lines could be oriented and defined so as to coincide with the found lanes.


### 2. Identified shortcomings of the current pipeline


A primary shortcoming of this method used in draw_lines() was the handling of slopes with a value of 0. This resulted in Nan being reported and disrupted the drawing of annotated lines, which deviated from the correct lane orientations. This occured when a slope, m = 0 was calculated. This caused the pipeline to fail, but principly was only an issue on the second (challenge) video. There were some options to address this, one was to find the segments of m = 0 and remove them, or to tune the parameters for the lines from the Hough Lines function. I worked mainly with parameter tuning, since it seemed that this would be the root of the problem. Parameter tuning worked well to avoid the Nan problem, although there are parts of the video with lines moving too much with slope deviations from the real lane lines. Additionally, tunning the parameters for the primary test and challenge videos showed that it was possible to get a good solution on the primary test videos, but the solution would fail on the challenge videos.

![alt text][fail001]


### 3. Possible improvements to the pipeline

Instead of defning a line based on drawing a linear line from the sorted slope values, another option may be to define the derivative at the mid-point of the found line in the region of interest, and average around that point. This should give a better instantaneous value and avoid the issues seen in the challenge video with curved lane lines, which prinicipally caused the method to fail.
