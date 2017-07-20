# Finding Lane Lines on the Road

---

## Goals

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on my work in a written report

## Reflection

### 1. Pipeline description

My pipeline consisted of 5 steps:

- First, I converted the images to grayscale
- Second, I use gaussian blur to reduce the noise
- Third, I got the edges by using canny algorithm
- Fourth, I got all hough lines according to canny edges, and simulated both left and right lane line
- Fifth, I overlying my lane line on top of original image

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function as follows:

- Distinguish left and right lane by *slope*. This work is done in `get_lane_line()` function
- Individually get all points of left line and right line in `get_end_points()`
- Using the points to do linear regression for both lines in `linear_regression()`. I made an assumption that `abs(slope)` will greater than `0.5` for both line. In order to make the over layer line start for the bottom top of the image, I extend the start point's `x` using: `x1 = (x1/3 if gradient <= 0 else x1)` for left line and `x2 = (x2*3 if gradient >= 0 else x2)` for right line

### 2. Potential shortcomings with current pipeline

One potential shortcoming would happen when the car entering a curved lane. Linear regression will absolutely not work according to `challenge.mp4`.

### 3. Possible improvements

A possible improvement would be classify both lines with a classifier like a *middle line*. I think this will be more accurate than slope calculating.

Another potential improvement could be to speed up the process. Now it can not catch up with the video rate. 
