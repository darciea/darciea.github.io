---
layout: page
title: MNIST Digit Classifier
description: End-to-end project to build, containerize, and deploy a digit recognition application.
img: assets/img/MNIST.png
importance: 1
category: current
related_publications: false
---

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/digit_recogniser.png" title="example image" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>


A personal project to design and deploy an end-to-end digit classification system using the MNIST dataset. The pipeline includes model development, web front-end integration, database logging, and full containerization for deployment on a self-managed server.

---

### 1. Model Development


Using PyTorch, two models were developed and trained locally:

- **Simple Neural Network:** Achieved 97.33% accuracy.
- **Convolutional Neural Network (CNN):** Achieved 98.42% accuracy. As expected, CNNs outperform standard feedforward networks in image-based tasks.


**Progress:**

- Preprocessing with normalization specific to the MNIST dataset.
- Implemented and compared multiple model architectures.
- Saved models for downstream use in the Streamlit interface.

**Next Steps:**

- Write a utility `predict()` function to streamline web integration.
- Store and version trained models for reproducibility.

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/MNIST.png" title="example image" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>


---

## 2. Interactive Web Front-End (Streamlit)

A Streamlit-based web application allows users to draw digits directly on a canvas. The image is preprocessed and passed to the model for real-time prediction.


**Progress:**

- Implemented an interactive canvas for digit input.
- Integrated the model to return predictions and confidence scores.

Include picture of interface.

**Next Steps:**

- Add functionality to compare predictions from different models.
- Improve UI layout and usability.
- (Optional) Embed a demo video or screenshots of the UI.

---

## 3. Data Logging (PostgreSQL)

All predictions made via the interface are logged to a PostgreSQL database. Logged data includes:
- Timestamp
- Predicted digit
- User-provided true label
- Confidence score
- Second-highest prediction (if initial prediction is incorrect)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/MNIST_SQL.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example of structured logs stored in PostgreSQL.
</div>

Note: While model accuracy is high on MNIST test data, real-world inputs from the canvas may degrade performance. Ongoing analysis of logged data helps identify these gaps.

---

## 4. Containerization (Docker)

All components of the application — PyTorch service, Streamlit app, and PostgreSQL — have been containerized using Docker.

- **Streamlit App Dockerfile**: A Dockerfile has been created for the Streamlit app, allowing it to run with all the necessary dependencies.
  
- **PostgreSQL Database Containerization**: A PostgreSQL database is also containerized with Docker, which includes persistent volumes for data storage. This ensures that database data persists even if the container is restarted.

- **Docker Compose**: Docker Compose is used to orchestrate the multi-container application, managing both the Streamlit frontend and PostgreSQL database. The Compose file includes environment variables for PostgreSQL credentials and the application, facilitating the setup of the entire stack with a single command.

- **Docker Volumes**: Volumes are used to persist PostgreSQL data. This ensures that even if the container is restarted or destroyed, the data remains intact.

---

## 5. Deployment

The final system has been deployed using **Render** for hosting and **Supabase** for PostgreSQL (as these are free resources). Docker Compose handles the orchestration of services. The system is designed to be publicly accessible via domain or IP and provides an end-to-end solution for MNIST digit classification.

- **Supabase Integration**: The PostgreSQL database, initially running within a Docker container, has been moved to **Supabase** for production purposes. This allows the app to use a managed cloud database while keeping the rest of the stack containerized.

- **Render Deployment**: The application is deployed on **Render**, a cloud platform that supports Docker-based deployments, making it easy to scale and manage the application in a production environment.

The final product is available to view at:  
[https://mnist-digit-classifier-b4sz.onrender.com/](https://mnist-digit-classifier-b4sz.onrender.com/)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/MNISTfinal.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    Preview of the deployed product!
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/supabase.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    Capture of the database as currently held in Supabase :)
</div>


---

This project introduced me to a full-stack ML application lifecycle — from model training to real-world deployment. It was a valuable learning opportunity in DevOps, containerization, and interactive user interfaces for ML applications.

**Additional Thoughts:** As the MNIST dataset is a collection of handwritten data, using the model on the digits drawn on the drawable canvas means that the predictions are extrapolated, and therefore does not have the greatest accuracy. While I achieved my goal of carrying out an end-to-end application, there are definitely a few improvements that could be made, such as saving the images to allow the model to learn from its errors. Maybe next time!
