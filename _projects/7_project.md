---
layout: page
title: Computer Vision + Robot Locomotion
description:
img: assets/img/4.jpg
importance: 1
category: previous
related_publications: false
---

This project extends the first assignment by integrating computer vision and mobile robot locomotion. The goal is to extract path features from a spatial map and navigate a mobile car with an onboard manipulator along a specified route.

## Requirements

<img src="https://github.com/user-attachments/assets/897a634e-27cb-4da5-9869-7ca906f1ec6a" width="500">

- **Path & Markers:**

  - Start (A) and end (B) points are marked in blue.
  - Road path is outlined in red.
  - Final target (C) is marked in green; the manipulator must reach it.

- **Mobile Robot Design:**
  - Car can have any wheels and actuators.
  - Should not exceed one-quarter of the road width.
  - Wheel diameters are of your choice.

## Tasks

1. **Path Identification:** Detect three markers (A, B, and C) and extract road boundaries.
2. **Car Navigation:**
   - Position the car at point A.
   - Actuate wheels to follow the path to point B.
3. **Manipulator Activation:**
   - At point B, move the manipulator to reach the green target (C) at any feasible altitude.

## My Solution

Given the original image, a close examination of the greyscale image reveals that the image is overexposed, making distinction of the markers difficult, especially the green marker that blends in with the rest of the spatial map once in grayscale.

<img src="https://github.com/user-attachments/assets/498f296f-626d-43a3-b6b9-6836c8d4833c" width="500">

Redistribution of the grey levels results in Figure 2 which makes it much easier to select the sections of interest from the image, as the markers are now quite clearly the darkest parts of the entire image.

<img src="https://github.com/user-attachments/assets/98fd526f-64ba-45b5-9d0c-ad0ec5a264da" width="500">

<img src="https://github.com/user-attachments/assets/1e78b9e4-3fe3-46a2-b03b-7bfb48b54025" width="250">

In selecting the darkest grey levels, other shapes are also chosen, and thus to further extract the markers alone, their circular nature comes into play. Here erosion followed by dilation is performed, to extract solely the markers, and then to restore them to their original size.

<img src="https://github.com/user-attachments/assets/cf70cbfc-f337-4500-86ea-52522a3db9e5" width="500">

The path to be taken is shown to be within the two red lines in the original picture. Obtaining the red lines is not a difficult task as they feature in the darkest grey levels of the original overexposed image, and so a new image consisting only of the darkest section is brought forward. The Hough transform is then applied to identify the lines present in the image, with the ρ and θ values corresponding to the lines present in the whitest points of the transform.

<img src="https://github.com/user-attachments/assets/ac0aadd4-7784-4545-a23f-36eeba37884b" width="500">

The values extracted from the Hough transform led to the following lines:

<img src="https://github.com/user-attachments/assets/9410da7b-c94f-47ab-8fed-0aab3577a07b" width="500">

The mobile robot section of this project is better viewed from the pdf files above.
