---
layout: page
title: Robotic vision
description: Extracting path features from a spatial map and navigate a mobile car.
img: assets/img/compvis.jpg
importance: 1
category: previous
related_publications: false
---

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/map.jpg" title="example image" class="img-fluid rounded z-depth-1 w-50" %}
    </div>
</div>

This project involved extracting path features from a spatial map and navigating a mobile car with an onboard manipulator along a specified route. Shown here is the methodology for path identification where the aim was to detect three markers (A, B, and C) and extract road boundaries.

**Path Identification:**

Given the original image, a close examination of the greyscale image reveals that the image is overexposed, making distinction of the markers difficult, especially the green marker that blends in with the rest of the spatial map once in grayscale.

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/overexposed.jpeg" title="example image" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>

Redistribution of the grey levels results in Figure 2 which makes it much easier to select the sections of interest from the image, as the markers are now quite clearly the darkest parts of the entire image.

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/redistributed.jpeg" title="example image" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>

In selecting the darkest grey levels, other shapes are also chosen, and thus to further extract the markers alone, their circular nature comes into play. Here erosion followed by dilation is performed, to extract solely the markers, and then to restore them to their original size.

<div class="container" style="max-width: 80%; margin: 0 auto;">
  <div class="row">
    <!-- First image (2/3 of the width) -->
    <div class="col-md-4 mt-3 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/darkest.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <!-- Second image (1/3 of the width) -->
    <div class="col-md-8 mt-3 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/markers.jpeg" title="example image" class="img-fluid rounded z-depth-1 w-100" %}
    </div>
  </div>
  <div class="caption text-center mt-2"> Markers extracted, then eroded and dilated. </div>
</div>

The path to be taken is shown to be within the two red lines in the original picture. Obtaining the red lines is not a difficult task as they feature in the darkest grey levels of the original overexposed image, and so a new image consisting only of the darkest section is brought forward. The Hough transform is then applied to identify the lines present in the image, with the ρ and θ values corresponding to the lines present in the whitest points of the transform.

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Hough.jpeg" title="example image" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>

The values extracted from the Hough transform extracted the lines of the path, from which finding the median allowed the path to be taken to be identified.

<div class="container" style="max-width: 80%; margin: 0 auto;">
  <div class="row">
    <!-- First image (2/3 of the width) -->
    <div class="col-md-6 mt-3 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/Lines.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <!-- Second image (1/3 of the width) -->
    <div class="col-md-6 mt-3 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/path.jpeg" title="example image" class="img-fluid rounded z-depth-1 w-100" %}
    </div>
  </div>
</div>


