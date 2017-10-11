# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals of this project are :
* Make a pipeline that finds lane lines on the road
* Reflect on the work done in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve.jpg "Original Image"
[image2]: ./test_images_output/image_adjusted1.jpg "Gamma Correction"
[image3]: ./test_images_output/gray1jpg "Grayscale"
[image4]: ./test_images_output/yw_mask1.jpg "Yellow and White Mask"
[image5]: ./test_images_output/en_gray1.jpg "Enhanced gray"
[image6]: ./test_images_output/blur1.jpg "Gaussian"
[image7]: ./test_images_output/edges1.jpg "Canny"
[image8]: ./test_images_output/masked_edges1.jpg "ROI"
[image9]: ./test_images_output/lines.jpg "Hough"
[image10]: ./test_images_output/transparent_lines.jpg "Overlay"


---

### Reflection

### 1. Pipeline description

The pipeline proposed consists of 9 steps:

1. Gamma correction. The challenge video presented some inconsistent shades in the road, rendering more difficult the lane lines detection. By controlling brightness and contrast it was possible to make the lane markings more clearly visible.

![alt text][image2]

2. Grayscale conversion. The adjusted image is then converted into grayscale.

![alt text][image3]

3. White and yellow extraction. White and yellow pixels are extracted from the gamma adjusted image to create a mask.

![alt text][image4]

4. Grayscale image gradient enhancement. A bitwise OR operation is used to overlay the white mask pixels  into the gamma adjusted image.

![alt text][image5]

5. Gaussian blur. Gaussian noise filtering is applied.

![alt text][image6]

6. Canny edge detection. 

![alt text][image7]

7. Region of interest masking. The detectected edges are further filtered by masking a trapezoidal area.

![alt text][image8]

8. Hough transform is used to extract lines from the detected edges. In order to draw a single line on the left and right lane markings, I modified the draw_lines() function by separating the line segments corresponding to left and right lane markings and subesequently extracting the points corresponding to every line segment.
The points were stored in lists and fitted to a pair 1st order polynomials. The coefficients were used to determine the start and end points of the line segments to be draw the pair of lines.

![alt text][image9]

9. The lines are overlaid o

### 2. Potential shortcomings with the current pipeline


One potential shortcoming is already seen in the challenge video. The curvature of the lane lines cannot always would be aproximated to straight lines. 

Eventhough the pipeline has proven capable enough to handle different light conditions and changes in the line and roads colour shades, more complex road markings (e.g. pedestrian crossings) would be impossible to model with this approach.
...


### 3. Potential improvements 

Clothoidal curves or 3rd order polynomials would probably be a better fit for the shape of the lane lines. 

Another potential improvement could be to implement a different regression method (e.g. RANSAC) to filter outliers points that are unlikely be part of the lane lines.
