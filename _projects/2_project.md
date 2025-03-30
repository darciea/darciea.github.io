---
layout: page
title: ME4 Introduction to Robotics
description: Coursework completed
img: assets/img/Manip.png
importance: 2
category: previous
giscus_comments: false
---

## Part 1 Overview

This project involves designing and analyzing a simple robot with four degrees of freedom (DoF). The goal is to create a feasible design using readily available parts while applying kinematic principles to derive forward and inverse kinematics, the Jacobian, and trajectory planning.

## Requirements

- **Manipulator Design:** At least four moving joints, including one revolute and one prismatic joint.
- **Link Constraints:** At least two non-zero link offsets; last link must be an L-shaped rod.
- **Operational Space:** Robot stands on a plane, avoiding self-collisions.

## Tasks

1. **Design & Sketch:** Create a hand-drawn or CAD sketch with dimensions.
2. **Kinematics Analysis:**
   - Define Denavit-Hartenberg (DH) parameters.
   - Derive forward and inverse kinematics.
3. **Jacobian Calculation:** Compute the Jacobian matrix.
4. **Trajectory Planning:** Develop an algorithm to move the end-effector between two points with ten via points.

## My solution

The application of this robotic manipulator is as an appliance in the kitchen, primarily to assist in stirring a cooking pot, or to mix a baking mixture, while there is also opportunity for other tasks to be undertaken, e.g. adding ingredients to the pot. The end-effector is an L-shaped rod pointing downwards, of which an attachment can allow it to hold a spoon or pincers to add items to add to the pot.

<img src="https://github.com/user-attachments/assets/0a284e1e-70a4-4147-8b30-44ec94107a25" width="500">

<img src="https://github.com/user-attachments/assets/d901f6dc-57cc-4056-a186-a75946a13f7c" width="500">

As the primary aim is to stir a pot, the manipulator’s main goals are to follow a loosely circular trajectory (imitating the motion of an arm as one might cook a stew). The end effector also can change height in order to place the spoon or utensil into and out of the bowl when instructed to do so.

<img src="https://github.com/user-attachments/assets/326897d2-1a65-4bba-8ac4-ade301ea9ca8" width="500">

<img src="https://github.com/user-attachments/assets/f4cef1ed-c44d-4a67-bf94-9ffe100aa75d" width="500">

The actual trajectory can be seen to deviate a fair amount from the ideal trajectory – this is likely due to the MATLAB spline function utilising a 3rd order polynomial, but since the shape in the X-Y plane is circular, it is intuitive that it would be best modelled by a quadratic function, so increases in the polynomial will only introduce more fluctuations. However, for the purposes of this manipulator, a deviation from the exact circular path does not indicate a failure for the manipulator.

## Part 2 Overview

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
