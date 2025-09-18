# IRS-Sleep-Position-Prediction: A Non-Intrusive Stress Prediction System using Sleep Position Analysis and Infrared Imaging

<p align="center">
  <img src="./Outputs/Final/architecture.png" alt="IRS-Sleep-Position-Prediction Architecture" height="500">
  <br>
  <span style="font-size: 14px; color: gray;"><b>System Architecture</b></span>
</p>

---

## 🔍 Overview

**IRS-Sleep-Position-Prediction** is a non-intrusive, computer vision–based system developed to estimate **stress levels from sleep positions** using **infrared imaging (IRS)** and **pose analysis**. This project was completed as part of an academic research initiative at **VIT Chennai**.

The system captures low-light IRS images, applies **YOLO-based landmark detection**, and fuses outputs from a **landmark feature regression model** and an **image-based transfer learning model**. By combining posture recognition with stress-level regression, the system offers a novel, secure, and real-time approach to health monitoring.

---

## 📜 Abstract

Sleep postures reflect underlying physiological and psychological conditions, making them valuable indicators of stress. Unlike intrusive methods (wearables, EEG sensors), this project leverages **infrared imaging** to capture natural sleep behavior in a secure and unobtrusive manner.

- **Pose Detection**: YOLOv11 detects and normalizes 17 landmarks per frame.  
- **Feature Engineering**: Distances, angles, spreads, and symmetry metrics are extracted from landmarks.  
- **Model Fusion**: Landmark-driven classifiers and transfer learning–based vision models are fused to improve robustness.  
- **Stress Estimation**: Posture predictions are aggregated over time to derive **stress scores**.  

This **fusion-driven approach** ensures accurate recognition of sleep postures and reliable stress estimation, addressing gaps in non-invasive health monitoring.

---

## ⚙️ Core Components

### 1. Dataset Acquisition
- IRS images of mannequins under low-light conditions using an **IR-selective camera**.  
- Images labeled into sleep posture classes: **Foetus, Log, Starfish, Yearner, Unknown**.  
- Dataset augmented and normalized for training landmark and vision-based models.

---

### 2. Pose Detection & Normalization
- **YOLOv11** identifies **17 body landmarks** (nose, shoulders, elbows, wrists, hips, knees, ankles).  
- Landmarks normalized relative to bounding box size.  
- Missing points imputed using **Euclidean similarity** or **mean replacement**.

<p align="center">
  <img src="./Outputs/Final/Dataset_Plots/Pose Recognition Sample.png" alt="Sample IRS Landmark Detection" height="300">
  <br>
  <span style="font-size: 14px; color: gray;"><b>Sample IRS Landmark Extraction</b></span>
</p>

---

### 3. Feature Extraction
From the 17 landmarks, the following features were derived:
- **Euclidean Distances**: between key joints (e.g., shoulder–elbow, hip–knee).  
- **Angles**: joint-based angular features.  
- **Symmetry Measures**: difference between left/right side landmarks.  
- **Spreads**: horizontal and vertical span of posture.  
- **Trigonometric Features**: sine/cosine transformations of angular metrics.

<p align="center">
  <img src="./Outputs/Final/Dataset_Plots/Scatter Plot of Landmarks.png" alt="Scatter Plot of Landmark Features" height="300">
  <br>
  <span style="font-size: 14px; color: gray;"><b>Scatter Plot of Landmarks</b></span>
</p>

---

### 4. Model Architecture
- **Landmark Model**: Extra Trees, SVM, Random Forest, MLP, and XGBoost tested.  
- **Vision Transformer (ViT)**: fine-tuned for IRS sleep posture recognition.  
- **Fusion Model**: Logistic Regression meta-classifier combining both outputs for optimal decision-making.  

---

### 5. Stress Estimation
- Detected sleep postures aggregated into **frequency distributions**.  
- Stress score derived as a weighted sum of posture occurrences across sleep duration.  
- Provides insights into **stress patterns** without requiring intrusive hardware.

---

## 🧪 Evaluation & Metrics

- **Accuracy**, **Precision**, **Recall**, **F1-score** calculated for pose prediction.  
- Stress estimation validated using regression error metrics.  

<p align="center">
  <img src="./Outputs/Final/Fusion_Model_Plots/Confusion matrix.png" alt="Confusion Matrix" height="300">
  <br>
  <span style="font-size: 14px; color: gray;"><b>Final Confusion Matrix</b></span>
</p>

---

## 📂 Repository Structure
IRS-Sleep-Position-Prediction/
│
├── Codes/
│ ├── Pose Classification - 2.ipynb
│ ├── Pose Classification - 3.ipynb
│ ├── Pose Recognition Test - 1.ipynb
│ ├── Pose Recognition Test - 2.ipynb
│ └── Pose Recognition Test - 3.ipynb
│
├── Outputs/
│ └── Final/
│ ├── Dataset_Plots/
│ │ ├── Bar Graph of Undetected Landmarks.png
│ │ ├── Box Plot - X Coordinate.png
│ │ ├── Box Plot - Y Coordinate.png
│ │ ├── Pose Recognition Sample.png
│ │ └── Scatter Plot of Landmarks.png
│ ├── Fusion_Model_Plots/
│ │ ├── Accuracy.png
│ │ ├── Clustered Classification Metrics.png
│ │ ├── Confusion matrix.png
│ │ ├── PR Bubble.png
│ │ └── PR Scatter.png
│ ├── Landmark_Model_Plots/
│ │ ├── KNN_1.png
│ │ ├── MLP_1.png
│ │ ├── random forest rv.png
│ │ ├── Random_Forest.png
│ │ ├── svm_1.png
│ │ └── XGBoost.png
│ └── architecture.png
│
└── README.md
