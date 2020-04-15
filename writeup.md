
# **Finding Lane Lines on the Road** 

## Goals Of The Project

The goal of the project is to build a lane finder using fundamental computer vision techniques. Then use it to detect lane in videos.

## Pipeline

[//]: # (Image References)
[image1]: ./writeup/output_19_1.png "Samples"
[image2]: ./writeup/output_26_0.png "Color Filtered"
[image3]: ./writeup/output_29_0.png "Canny"
[image4]: ./writeup/output_32_0.png "ROI"
[image5]: ./writeup/output_35_0.png "Hough"
[image6]: ./writeup/output_38_0.png "Overlay"

My piple line consisted of 5 steps.

I first picked some images from the test images and from the test videos, and experimented the pipeline on them. There were special cases with shadow and changing ground colors in the challenge video.

![alt text][image1]

First, a color filter was applied to extract white and yellow color. The results were shown as below.

![alt text][image2]

Then, I applied the canny edge detection on the filtered image. The image was first converted to grayscale and then a guassin filter was applied to remove noises.

![alt text][image3]

Next, a region of interest was applied to exclude area outside the road. The region of interest was a list of polylines. The position of vertices were defined using percentage to adpt different image sizes.

![alt text][image4]

After that, Hough line detector was applied to extract lines, with tuned parameters.

![alt text][image5]

The final step was processing, grouping, averaging the lines and displaying only two main lanes. In this step, I did not modify the draw function, instead, I modified the hough line function to make it return lines. The return lines were then passed to a process lines function to do the processing.

The lines were classified into left lane and right lane according to their slopes and center positions. After that, two result lines were computed using the least square fit with thier end points. They were then overlayed on the original image.

![alt text][image6]


## Video Results

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/3TwNHzvbq5g/0.jpg)](https://www.youtube.com/watch?v=3TwNHzvbq5g)

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/XonhMzo80g4/0.jpg)](https://www.youtube.com/watch?v=XonhMzo80g4)

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/3qYUok4jDIg/0.jpg)](https://www.youtube.com/watch?v=3qYUok4jDIg)


## Potential Shortcomings and Improvements

One potential shortcoming is the pipeline is only detecting yellow and white lanes. If there are lanes in other colors, the current pipeline will fail to detect them. The improvement can be using the full color image, or try different color space such as HSV space.

Another potential shortcoming is the final line fitting is using the least square fit, therefore, some small line segment outliers can make the line fitting unstable. One improvement can be using RANSAC to do much robust line fitting.

One future improvement of the pipleline can be utilizing the video frames. One can take the past N frames of the video and do averaging, filtering base on the past N frames, which cloud potentially give better results.