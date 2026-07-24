Skin Lesion Classification Using Deep Learning

A deep learning project for classifying dermoscopic skin-lesion images from the HAM10000 dataset into seven diagnostic categories.

The project compares custom convolutional neural networks with MobileNetV2 transfer learning and fine-tuning. It also includes a Gradio web interface that allows users to upload a skin-lesion image and view the predicted class probabilities.

Project Overview

Skin-lesion classification is challenging because several skin conditions have similar visual characteristics. The HAM10000 dataset is also highly imbalanced, with melanocytic nevi representing most of the available images.

This project builds and evaluates four deep learning models:

Simple CNN baseline
Improved CNN with class weighting
MobileNetV2 transfer learning
Fine-tuned MobileNetV2

The models are compared using:

Test accuracy
Macro precision
Macro recall
Macro F1-score
Weighted F1-score
Macro AUC
Weighted AUC
Classification reports
Confusion matrices

Because of class imbalance, macro F1-score was used as the main metric for selecting the best model.

Dataset

The project uses the HAM10000: Human Against Machine with 10,000 Training Images dataset.

The notebook processes:

10,015 dermoscopic images
7 skin-lesion classes
Metadata from HAM10000_metadata.csv
Images from two separate image folders
Dataset Split

A stratified split was used to preserve the class distribution across all subsets.

Dataset subset	Percentage	Number of images
Training	70%	7,010
Validation	20%	2,003
Testing	10%	1,002

The random state was set to 42 for reproducibility.

Model 1: Simple CNN Baseline

The baseline model contains:

Three convolutional layers
Max-pooling layers
Flatten layer
Dense layer with 128 neurons
Dropout
Seven-class softmax output layer

Model 2: Improved CNN

The improved CNN contains:

Four convolutional blocks
Batch normalization
Max pooling
Global average pooling
Two dense layers
Dropout regularization
Class weights

Class weights were calculated using the balanced class-weight method to give more importance to minority classes.
Model 3: MobileNetV2 Transfer Learning

This model uses MobileNetV2 pretrained on ImageNet as a feature extractor.

The MobileNetV2 base is initially frozen and connected to:

Global average pooling
Dense layer with 256 neurons
Dropout
Dense layer with 128 neurons
Dropout
Seven-class softmax output layer
Model 3B: Fine-Tuned MobileNetV2

The best MobileNetV2 transfer-learning model is loaded and fine-tuned.

Fine-tuning settings include:

Last 40 MobileNetV2 layers considered for fine-tuning
Batch-normalization layers kept frozen
26 MobileNetV2 layers made trainable
Adam optimizer
Learning rate: 0.00001
Maximum of 10 fine-tuning epochs
Balanced class weights
Early stopping
Learning-rate reduction


Gradio Web Application

The notebook includes an interactive Gradio interface.

The application can:

Load the saved best model
Display the preprocessing workflow
Show model architectures and results
Display accuracy and loss curves
Display confusion matrices
Show classification reports
Compare all trained models
Upload a skin-lesion image
Predict one of the seven classes
Display probabilities for all classes



