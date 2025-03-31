---
layout: page
title: Robotics Manipulator
description:
img: assets/img/Manip.png
importance: 2
category: previous
giscus_comments: false
---

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
