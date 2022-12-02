---
layout: post
title:  "PPM File Adjustment Algorithms"
date:   2022-11-20 13:50:39
categories: algorithms
---
<small>Because of code confidentiality, this page only demonstrates the framework</small>
<br>
<h1>PPM File Adjustment Algorithms</h1>
The primary image resizing algorithm is based on a seam-carving algorithm. The task of the algorithm set is to apply seam carving for content-aware resizing of images. The core algorithm works by finding and removing “seams” in the image that pass through the least important pixels. For a quick introduction, check out [this video][video-link].
<br>
<br>
For example:
![cv-demo](/static/projects/pv-demo.png)
<br>
<h2>Table of Content</h2>
1. Fundations of objects
2. Basic functions and algorithms
3. Examples of effects
<br>
<br>
<h2>1. Fundations of Objects</h2>
<h3>RGB Pixel</h3>
Each Pixel includes three integers, which represent red, green, and blue (RGB) color components. Each component takes on an intensity value between 0 and 255. The Pixel type is considered “Plain Old Data” (POD), which means it doesn’t have a separate object interface. Here is the Pixel struct and some examples:
![rgb_pixel_demo](/static/projects/PPM-Adjustment/rgb.png)
<br>
<h3>RGB Image</h3>
An RGB image here is considered a matrix of RGB pixel(s). A matrix is a two-dimensional grid (grid[row_num][column_num]). Below is a 5x5 image and its conceptual representation as a grid of pixels:
![rgb_grid_demo](/static/projects/PPM-Adjustment/rgb-image.png)
<br>
<h3>PPM Format File</h3>
Here’s an example of an Image and its representation in PPM:
![ppm_demo](/static/projects/PPM-Adjustment/ppm file.png)
<br>
<br>




[video-link]:  https://www.youtube.com/watch?v=6NcIJXTlugc
