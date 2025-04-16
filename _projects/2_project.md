---
layout: page
title: Robotics Manipulator
description: Designing a 4 DoF manipulator and deriving its kinematics.
img: assets/img/Manip.png
importance: 2
category: previous
giscus_comments: false
---

<div class="text-center my-3">
  <img src="https://github.com/user-attachments/assets/0a284e1e-70a4-4147-8b30-44ec94107a25" width="500" class="img-fluid rounded">
</div>

This project involves designing and analyzing a simple robot with four degrees of freedom (DoF). The goal is to create a feasible design using readily available parts while applying kinematic principles to derive forward and inverse kinematics, the Jacobian, and trajectory planning.

---

The application of my robotic manipulator is in a **kitchen setting**, designed to assist in tasks such as **stirring a cooking pot** or **mixing ingredients**. The end-effector is an L-shaped rod pointing downward, designed to hold tools like a spoon or pincers.

<div class="row justify-content-center mb-4">
  <div class="col-md-6 text-center">
    {% include figure.liquid 
      loading="eager" 
      path="assets/img/Frames.png" 
      title="example image" 
      class="img-fluid rounded z-depth-1 w-100" 
    %}
  </div>
  <div class="col-md-5 text-center">
    {% include figure.liquid 
      loading="eager" 
      path="assets/img/Cartesianframes.png" 
      title="example image" 
      class="img-fluid rounded z-depth-1 w-100" 
    %}
  </div>
    <div class="text-muted small mt-2">Illustration of the frames and their corresponding Cartesian positions in the system.</div>
</div>

As the primary goal is to stir, the manipulator aims to follow a **loosely circular trajectory** — imitating the human stirring motion. It can also adjust its vertical height to insert or remove utensils from the bowl.

<div class="row justify-content-center mb-4">
  <div class="col-md-6 text-center">
    {% include figure.liquid 
      loading="eager" 
      path="assets/img/birdseyemanip.png" 
      title="example image" 
      class="img-fluid rounded z-depth-1 w-100" 
    %}
  </div>
  <div class="col-md-5 text-center">
    {% include figure.liquid 
      loading="eager" 
      path="assets/img/birdseyecircle.png" 
      title="example image" 
      class="img-fluid rounded z-depth-1 w-100" 
    %}
  </div>
      <div class="text-muted small mt-2">Joint configuration and axis orientation.</div>
</div>

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3dtrajectory.png" title="example image" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
        <div class="text-muted small mt-2">Illustration of the via points used for trajectory planning - modelling the initial stirring motion.</div>
</div>

