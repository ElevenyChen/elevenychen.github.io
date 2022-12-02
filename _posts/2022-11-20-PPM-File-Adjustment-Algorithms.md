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
4. Potential improvment
<br>
<br>
<h3>1. Fundations of Objects</h3>
<h4>RGB Pixel</h4>
Each Pixel includes three integers, which represent red, green, and blue (RGB) color components. Each component takes on an intensity value between 0 and 255. The Pixel type is considered “Plain Old Data” (POD), which means it doesn’t have a separate object interface. Here is the Pixel struct and some examples:
![rgb_pixel_demo](/static/projects/PPM-Adjustment/rgb.png)
<br>
<h4>RGB Image</h4>
An RGB image here is considered a matrix of RGB pixel(s). A matrix is a two-dimensional grid (grid[row_num][column_num]). Below is a 5x5 image and its conceptual representation as a grid of pixels:
![rgb_grid_demo](/static/projects/PPM-Adjustment/rgb-image.png)
<br>
<h4>PPM Format File</h4>
Here’s an example of an Image and its representation in PPM:
![ppm_demo](/static/projects/PPM-Adjustment/ppm file.png)
However, to process color information more efficiently, each color's channel is stored seperately.
The Image struct looks like this:
{% highlight ruby %}
struct Image {
  int width;
  int height;
  Matrix red_channel;
  Matrix green_channel;
  Matrix blue_channel;
};
{% endhighlight %}
<br>
<br>
<h3>2. Basic Functions and Algorithms</h3>
<h4>Read in and save</h4>
Read in PPM Format files correctly, and create the corresponding dynamic objects.
<br>
<h4>Rotate and resize images</h4>
<br>
<h4>Processing: The seam carving algorithm</h4>
<p>The seam carving algorithm works by removing seams that pass through the "least important" pixels in an image. We use a pixel’s energy as a measure of its importance.</p>
<p>To compute a pixel’s energy, we look at its neighbors. We’ll call them N (north), S (south), E (east), and W (west) based on their direction from the pixel in question (we’ll call it X).</p>
![energy-matrix_demo](/static/projects/PPM-Adjustment/energy_matrix.png)
The energy of X is the sum of the squared differences between its N/S and E/W neighbors:
{% highlight ruby %}
energy(X) = squared_difference(N, S) + squared_difference(W, E)
{% endhighlight %}
<p> We do a in-depth search. First we read in a new pixel, record the energy(X). When we find a new pixel each time we read, we put it in the searcing container. The search process should follow a "first in first out" rele.</p>
<p>Once the energy matrix has been computed, the next step is to find the path from top to bottom (i.e. a vertical seam) that passes through the pixels with the lowest total energy (this is the seam that we would like to remove).We would want to choose the least costly from those pixels, which means the minimum cost to get to a pixel is its own energy plus the minimum cost for any pixel above it. This is a recurrence relation. For a pixel with row r and column c, the cost is:</p>
{% highlight ruby %}
cost(row, column) = energy(row, column) + min(cost(row-1, column-1),
                                cost(row-1, column),
                                cost(row-1, column+1))
{% endhighlight %}
<p> The seam array passed into this function contains the column numbers of the pixels that should be removed in each row, in order from the top to bottom rows. To remove the seam, copy the image one row at a time, first copying the part of the row before the seam (green), skipping that pixel, and then copying the rest (orange).</p>
![seam_demo](/static/projects/PPM-Adjustment/remove.png)
<br>
<br>
<h3>Examples of Effects</h3>
Small Example: dog
![dog_ori](/static/projects/PPM-Adjustment/dog/dog.ppm)







[video-link]:  https://www.youtube.com/watch?v=6NcIJXTlugc
