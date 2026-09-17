# 🔥 Skin Burn Prediction

A deep learning image classification project that predicts the degree of a skin burn from an uploaded image.

The project uses **TensorFlow/Keras** for model development and **Streamlit** to provide a simple web interface for making predictions.

> ⚠️ **Disclaimer:** This project is for educational and research purposes only. It is not a medical diagnostic tool and should not be used as a substitute for professional medical advice.

## 📌 Overview

The goal of this project is to classify skin burn images into three categories:

- **First Degree**
- **Second Degree**
- **Third Degree**

The project initially explores a CNN model trained from scratch and then improves the approach using **transfer learning with MobileNetV2** pretrained on ImageNet.

The final trained model is saved as a Keras `.h5` model and integrated into a Streamlit application.

## 🧠 Model

The final model uses **MobileNetV2** as the pretrained base model.

The MobileNetV2 feature extractor is followed by a custom classification head:

- MobileNetV2 pretrained on ImageNet
- Global Average Pooling
- Dense layer with 256 units
- ReLU activation
- Batch Normalization
- Dropout with a rate of 0.5
- Dense output layer with 3 classes
- Softmax activation

The MobileNetV2 base model is initially frozen during training.

The model contains approximately **22.25 million parameters**.

### Training Configuration

- **Optimizer:** Adam
- **Loss Function:** Categorical Crossentropy
- **Metric:** Accuracy
- **Input Size:** 224 × 224 × 3
- **Output Classes:** 3

## 📊 Dataset

The project uses the **Skin Burn Dataset** from Kaggle.

The dataset contains images belonging to three burn-degree classes:

- First Degree: **532 images**
- Second Degree: **490 images**
- Third Degree: **201 images**

Because the classes were imbalanced, the minority classes were oversampled so that each class contained **532 images**.

The resulting dataset was divided into:

- **80% Training**
- **20% Validation**

### Data Augmentation

Training images were augmented using:

- Rotation
- Width shifting
- Height shifting
- Shearing
- Zooming
- Horizontal flipping

Validation images were rescaled without augmentation.

## 📈 Results

The initial CNN model trained from scratch achieved a validation accuracy of approximately **51.34%**.

After applying transfer learning with MobileNetV2, the final model achieved a recorded validation accuracy of **81.25%**.

The notebook also includes:

- Confusion matrix
- Classification report
- Per-class evaluation

These evaluations provide additional information about how the model performs across the three burn-degree classes.

## 🖼️ Image Preprocessing

Before an uploaded image is passed to the model, it goes through the following preprocessing steps:

1. The image is loaded using Pillow.
2. The image is resized to **224 × 224 pixels**.
3. The image is converted into a NumPy array.
4. A batch dimension is added.
5. Pixel values are normalized by dividing them by 255.

This produces the input format expected by the trained model.

## 🚀 Streamlit Application

The project includes a Streamlit application that allows users to classify burn images through a web interface.

The user can:

1. Upload a `.jpg`, `.jpeg`, or `.png` image.
2. Preview the uploaded image.
3. Click the **Classify** button.
4. Receive the predicted burn-degree class.

The application loads:

- `burns_prediction_model.h5` — the trained model
- `class_indices.json` — the class mapping

## 📁 Project Structure

```text
Skin-Burn-Prediction/
│
├── skin_Burn_Prediction(2).ipynb
├── main.py
├── burns_prediction_model.h5
├── class_indices.json
└── README.md
