#**FINDING ROAD LANE LINES PROJECT**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

###***Reflection***

###1. Pipeline Description
I took the following steps to build my pipeline. 
* Read input image and convert to numpy array
  - This is a basic step done with the imported python package _matplotlib.image_
* Obtain white and yellow color masks 
  - I added this function to helper functions in order to calculate the white and yellow masks
* Convert white/yellow mask image to gray scale using helper functions 
  - Using helper function _gray_ convert the white/yellow masked image to gray scale image
* Define a kernel size and apply Gaussian blur from helper functions
  - Using helper function apply Gaussian blur to the gray output image
* Define thresholds and apply Canny edge detection
  - Using helper function, defined the low and high thresholds and obtain Canny edges using the blurred gray output image
* Define a region of interest using vertices 
  - Using the the shape of the image, define some vertices to apply a region of interest where lines should be identified
* Apply Houghlines with defined parameters to Canny edges output image 
  -Using th helper functions, take the Canny edges output and obtain the lines in the region of interest using the Houghlines function
* Apply weights to Houghlines output against the original input image
  - Using helper function weighted_img apply weights for Houghlines output image and the original input image to create the final output image with lane lines drawn
  
Final output is the following:

[//]: # (Image References)

[image1]: ./test_images/lane_lines_final.png "Final output"

![alt text][image1]

To be able to produce the above output, I added the following methods to helper functions.
These methods are called from within _draw\_lines()_ 
* _slope\_intercept\_avg()_
   - Calculates the slope and intercept for each line found in Houghlines
   - Using left (negative slope) or right(positive slope) to separate each lane line
   - Calculate line length
   - Applies weights to longer lines
   - Returns output as (slope, intercept)
* _pixel\_line\_points()_
   - Converts from (slope, intercept) to point form (x1, y1)
* _lane\_lines()_
   - Calls _slope\_intercept\_avg()_ to obtain lane lines
   - Calls _pixel\_line\_points()_ to convert back to point form 
   - returns one single line

###2. Potential Short Commings
For the video challenge, I was able to run my pipeline on a subclip (5 sec) of the video. I have added 
the video to the notebook. The challenge video brought out many short comings from my pipeline, here are
some of the things that I noticed affected the pipeline 
* The curve, which produces an arc in the yellow and white lines. This results in the miscalculation of the line slope
and might need to use other nonlinear method to care of curves when calculating lines
* The change of color in the pavement causes the white dotted lines to be harder find  by the pipeline
* The shadow in the front of the road causes a similar effect to that of the pavement color

###3. Potential Improvements
May be apply another color selection to take care of the change of color in the pavement from dark to light
gray. I would add more weight to the white color mask as a starting point.
As mentioned aboved, I would use a nonlinear method to calculate the lines that can 
take care of curves. 
