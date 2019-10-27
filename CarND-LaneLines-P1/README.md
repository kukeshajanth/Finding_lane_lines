# **Finding Lane Lines on the Road** 



[//]: # (Image References)

[image1]: ./test_images/solidWhiteRight.jpg "Raw"

[image2]: ./pipeline_image/gray.jpg "Grayscale"

[image3]: ./pipeline_image/blur_gray.jpg "Gaussian_Blur"

[image4]: ./pipeline_image/canny.jpg  "Canny_detected_edges"

[image5]: ./pipeline_image/roi.jpg "Region_of_interest"

[image6]: ./pipeline_image/hough.jpg "Hough_transformed"

[image7]: ./pipeline_image/final.jpg "Final_image"
---

### Reflection

### 1.Pipeline.

My pipeline consisted of following steps. 

First, load in the image.

![alt text][image1]

Then, convert to grayscale image.

![alt text][image2]

Applying, gaussian blur to the gray scale image to smoothen it.

![alt text][image3]

To detect the edges in the image, canny filter is applied on the image.

![alt text][image4]

Then, the region of interest is masked, such that, region outside of the interest area is set to value 0.

![alt text][image5]

The roi region is converted into hough space to obtain lines and to extrapolate the line, I have found the slope and intercept for line on left and right(using positive and negative slope to differentiate). Then, used the mean of right and left slope and intercept to calculate the position of x corresponding to y.(We know the value of y as it mvalue starts from bottom of the image(image.shape[0]) to the value of y according to roi at top). Finally, line is draw between two points.

![alt text][image6]

Finally, this hough transformed image is added to the original image.

![alt text][image7]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be model is able to predict the line on a stright or slightly bent roads, as I have made extrapolation based on line formed using same slope and intercept. So, the model performs poorly on curved roads. 

Another shortcoming could be the region of interest I chose,which is subjective, might not perform well for all situations.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use polynomial function rather than linear

Another potential improvement could be to use deep learning, by providing large sets of annotated images, network would learn the best possible polynomial fit to represent the detected line whether it is a straight line or a curved line. 
