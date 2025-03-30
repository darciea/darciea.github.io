---
layout: page
title: MNIST Digit Classifier
description: Personal project to build a small, end-to-end application on a self-managed server by building, containerizing and deploying an MNIST digit classifier.
img: assets/img/MNIST.png
importance: 1
category: current
related_publications: false
---

## 1. Developing Pytorch model

This will be trained locally, and with the MNIST dataset, a high level of accuracy ~95% should be achievable. I will develop a couple of models (a simple neural network and a convolutional neural network), just to play around and get familiar with Pytorch.

### Progress

- Normalising the data according to MNIST dataset
- Created a Simple Linear NN and achieved 97.33% accuracy on the MNIST dataset
- Created a Convolutional NN and achieved 98.42% accuracy - ConvNets are better for Image processing

### Improvements

- Write a predict function for easy implementation for the Streamlit section
- Save various models for loading into the Streamlit

![image](https://github.com/user-attachments/assets/4ce0063d-1117-4b27-ba88-94ce45800f05)

![image](https://github.com/user-attachments/assets/e0a56930-5aa3-4c9d-8dfb-d9995dba79b3)

## 2. Creating an Interactive Front-End

I will create a web interface (Streamlit) so that users can draw a digit on a canvas or input area that will be input into the model, obtaining the prediction, confidence and receive the true label to gather feedback.

### Progress

- Have created the drawable canvas and preprocessed the resulting image
- Have implemented the model to make predictions on the image and return the prediction and confidence in the prediction

### Improvements

- Create sections to allow results back from different models for the same image to compare predictions
- Improve the readability / layout

https://github.com/user-attachments/assets/f9194d9e-38d4-4b02-bc63-45bd8292111a

## 3. Logging the attempts into a PostgreSQL database

Each time a prediction is made, the details are logged into a PostgreSQL database, including the timestamp, predicted digit, user-provided true label, confidence and, if the predicted digit does not match the true label, then the second highest probability guess is also recorded.

![image](https://github.com/user-attachments/assets/5612cda4-962c-4726-b835-e5daeb6754c0)

It is also important to note that while the Pytorch models performed well with high accuracy on the test dataset, we are extrapolating by using that model on the images provided by the drawable canvas. While normalised in the same way, there is a clear discrepancy between how the model performs on the images provided by the web interface. Further inspection of the database will likely reveal where the discrepancies are.

# Left to do

## 4. Containerization

The Pytorch model/service, Streamlit web app and PostgreSQL databas will be containerized into Docker. Docker Compose will then me used to define the multi-container setup in a docker-compose.yml file.

## 5. Deployment

The deployment end-to-end will be controlled on a self-managed server where Docker can be installed. The containerized application will then be deployed to this server which will then be made accessible via a public IP or domain.
