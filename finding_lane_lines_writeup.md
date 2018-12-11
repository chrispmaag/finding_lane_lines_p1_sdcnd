*Finding Lane Lines on the Road*

[![Finding Lane Lines](/images/youtube_snapshot.png)](https://youtu.be/XQAB_ylnxq0)

The goals of this project was to make a pipeline that finds lane lines on the road.

---

### 1. Pipeline Summary

My pipeline consisted of several steps. First, I converted the images to grayscale.
Then, I applied a Gaussian blur to help with generalization. Next up was Canny
edge detection to detect strong pixel gradients (edges). I followed this with a region
of interest mask to focus only on edges on the road directly in front of the car.
After that, I connected the dots (edges) from Canny edge detection using a Hough
line transform.

In order to draw a single line on the left and right lanes, I modified the
draw_lines() in several ways. First, for each line segment detected by the
Hough function, we calculate the slope and center of the line. Then, we examine
whether the slope is positive or negative and assign it to either the left or
right lane line. After taking the average across all the values in the respective
left and right sides, we solve for the missing value in y-y' = M(x-x'). Finally,
we use OpenCV's line function to draw these average lines onto the original image.

Here is a sample input image:

![Input Image](/images/whiteCarLaneSwitch.jpg)

With lane lines detected:

![Image With Lane Line Segments](/images/output_whiteCarLaneSwitch.jpg)

With projected lane lines:

![Output Image With Projected Lane Lines](/images/output_line_whiteCarLaneSwitch.jpg)


### 2. Potential Shortcomings With Current Pipeline

One potential shortcoming would be the heavy dependence on lighting conditions.
When the lane lines are difficult to see, the current pipeline struggles. This
could occur from wear on the road, changing concrete colors, or shadows.

Another potential shortcoming would be the expectation of finding lanes on the road
with no cars directly in front. A car in front of the camera would create more
line segments that could alter the calculated slope of the projected lane lines.


### 3. Possible Improvements To Pipeline

A possible improvement would be to further refine the allowable slopes of the
lane lines. Another potential improvement could be to change from Red Green Blue
(RGB) to Hue Lightness Saturation (HLS) color space to detect lane
lines under different lighting conditions.
