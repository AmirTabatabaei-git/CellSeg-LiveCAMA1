# CellSeg-LiveCAMA1
This is an algorithm for detecting and segmenting cells in live cell images of the CAMA-1 cell line.

### Introduction:

The aim of this project is to obtain a foreground mask of cells, then finding the cell locations for detecting the cell boundaries and segmenting cells in live cell images. Three different cell images are provided in this assignment. Also, a .txt ground truth foreground mask file is provided for all three images to assess the precision, recall, and F1-score metrics for our obtained mask. Aiming to do so, we used Scikit-image and OpenCV libraries in Python programming language to read and process each image. For each part of assignment, there are different steps are followed for segmenting the images at the end. We will explain them in following sections.

# **Part 1**

The task is to obtain a foreground mask for an RGB image, where foreground pixels are labeled with 1 and background pixels with 0. The provided code implements a method to achieve this task. In this report, we will present a detailed explanation of the implemented method, the selection of its parameters, visual results for the provided images, and quantitative metrics to evaluate the performance.

### Method:
The provided code implements the following method to obtain a foreground mask:
- Load the image and convert it to grayscale.
- Apply Gaussian blur to reduce noise in the image.
- Threshold the image using a threshold value of 170 and invert the binary image.
- Find the contours of the foreground objects in the binary image.
- Fill the holes in the binary image.
- Compare the obtained mask with the ground truth mask to calculate precision, recall, and F-score.

### Parameters:
The method takes one input, the path of the RGB image, and one optional parameter, the path of the ground truth mask. The parameter for Gaussian blur is (11,11), and the threshold value is 170. The default settings are used for filling the holes in the binary image. The parameters for finding contours are cv2.RETR_CCOMP and cv2.CHAIN_APPROX_SIMPLE.

### Parameter Selection:
The value of the threshold is selected by trial and error. The value of 170 was found to work well for the provided images. The kernel size for Gaussian blur is selected as (11,11), which is a commonly used value for removing noise in images. The default settings for filling the holes in the binary image are used as they work well in most cases. The parameters for finding contours are selected based on their suitability for detecting contours with holes, which is common in natural images.

### Visual Results:
The provided code is tested on three images, and the obtained masks are visualized alongside the ground truth masks. The images and masks are shown in Table 1. As can be seen from the figure, the obtained masks closely match the ground truth masks.

![Table 1](https://github.com/AmirTabatabaei-git/CellSeg-LiveCAMA1/assets/132440248/84a6ce9e-5794-4f83-a2af-fbf4546ca4dd)

###  Quantitative Metrics:
The quantitative metrics for evaluating the performance of the method are precision, recall, and F-score. The results for the three images are presented in Table 2. As can be seen from the table, the method performs well on all three images, with F-scores above 0.9 for all images.

<p align="center">
<img src="https://github.com/AmirTabatabaei-git/CellSeg-LiveCAMA1/assets/132440248/ea5b5662-c7cd-4bd2-ad4e-445211e45bea" width="450" height="130">

# **Part 2**

In the second part of the assignment, we need to find the approximate location of each cell by using distance transforms. The distance transform is an operator normally only applied to binary images. The result of the transform is a gray level image that looks similar to the input image, except that the gray level intensities of points inside foreground regions are changed to show the distance to the closest boundary from each point. For giving an example, when a distance transform is applied scaled by a factor of 3 it can be like the following images:

<p align="center">
  <img src="https://github.com/AmirTabatabaei-git/CellSeg-LiveCAMA1/assets/132440248/d90b675a-1e9a-4cb7-a3ec-3aef730bc754" width="250" height="80">
</p>


