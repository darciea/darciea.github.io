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

All components — PyTorch service, Streamlit app, and PostgreSQL — will be containerized using Docker.

**Planned Setup:**

- Dockerfiles for model service and Streamlit frontend
- PostgreSQL container with persistent volumes
- Docker Compose file to orchestrate the stack

---

## 5. Deployment

The final system will be deployed on a self-hosted server using Docker Compose. The server will be publicly accessible via domain or IP.

**Planned Tasks:**

- Configure server firewall and DNS (if needed)
- Set up Docker Compose with appropriate environment variables and volumes
- Ensure auto-restart and uptime monitoring

---

This project demonstrates a full-stack ML application lifecycle — from model training to real-world deployment. It’s also a learning opportunity in DevOps, containerization, and interactive user interfaces for ML applications.
