# Lung-Cancer-Ultrasound-Diagnosis (In progress)
Intelligent system for lung cancer diagnosis based on transthoracic ultrasound image analysis.


# Computer-Aided Lung Cancer Diagnosis Using Transthoracic Ultrasound Images

This repository contains an academic project focused on the development of a computer-aided system for lung cancer diagnosis based on transthoracic ultrasound (TUS) image analysis.

The project investigates image processing techniques applied to lung ultrasound images with the goal of supporting the diagnostic process through automated lesion analysis and classification.

---

## 1. Introduction

### 1.1 General Context

Lung cancer is one of the leading causes of mortality worldwide, with a major impact on healthcare systems and patients’ quality of life. Early and accurate diagnosis is essential for selecting appropriate treatment strategies and improving survival rates.

Transthoracic ultrasound (TUS) is a non-invasive imaging technique used for the evaluation of pulmonary lesions, offering advantages such as accessibility, low cost, and the absence of ionizing radiation. Ultrasound imaging can provide relevant information regarding lesion shape, structure, and internal characteristics. However, interpretation of ultrasound images is highly dependent on the examiner’s experience, which may introduce subjectivity into the diagnostic process.

In recent years, advances in medical image processing and machine learning have enabled the development of computer-aided diagnosis systems capable of extracting quantitative information from medical images. Such systems can assist clinicians by providing objective indicators and reducing variability in image interpretation.

---

### 1.2 Objectives

The main objective of this project is the development of an automated system for the analysis and classification of lung ultrasound images, with the purpose of supporting lung cancer diagnosis.

The specific objectives include:
- preprocessing lung ultrasound images to reduce noise and improve image quality;
- automatic extraction of the ultrasound region of interest (ROI);
- segmentation of suspicious pulmonary lesions;
- analysis of lesion characteristics based on image features;
- preparation of the processed data for subsequent classification.

---

### 1.3 System Specifications

The developed system processes grayscale lung ultrasound images and follows a sequential processing pipeline. The workflow includes image preprocessing, extraction of the ultrasound field, lesion segmentation, and feature analysis.

The system is designed to operate automatically, minimizing user intervention, and to provide visual outputs that facilitate result interpretation by highlighting detected regions and lesion contours.

---

## 2. Dataset Understanding and Analysis

### 2.1 Data Type and Origin

The dataset used in this project consists of two-dimensional grayscale transthoracic ultrasound images acquired for pulmonary lesion assessment. Ultrasound imaging is widely used in clinical practice due to its non-invasive nature and real-time acquisition capabilities.

Despite these advantages, lung ultrasound images present specific challenges for automated analysis, which require careful examination of data characteristics prior to processing.

---

### 2.2 Characteristics of Lung Ultrasound Images

Lung ultrasound images are affected by speckle noise, low contrast, and intensity inhomogeneities. These characteristics can obscure lesion boundaries and complicate segmentation tasks.

Pulmonary lesions may exhibit irregular shapes, heterogeneous intensity distributions, and weak contrast relative to surrounding tissues. These factors make lung ultrasound image analysis more challenging compared to other medical imaging modalities.

---

### 2.3 Dataset Organization and Labeling

The dataset is organized into predefined classes corresponding to cancer and non-cancer cases. Image labeling enables the use of supervised learning approaches in later stages of the project and allows objective evaluation of system performance.

This organization facilitates direct comparison between the system output and the ground truth labels associated with each image.

---

### 2.4 Data Quality Analysis

Preliminary analysis of the dataset reveals significant variability in image quality. Some images present clearly defined structures, while others contain low-intensity regions or non-uniform patterns that can negatively affect automated processing.

Such variability highlights the importance of robust preprocessing and segmentation techniques to ensure consistent analysis across different image conditions.

---

## 3. Dataset Preprocessing

### 3.1 Image Filtering and Noise Reduction

Due to the presence of ultrasound-specific noise, multiple filtering techniques were evaluated to improve image quality while preserving relevant anatomical details. Median, Gaussian, and bilateral filters were tested during this stage.

Among these methods, Gaussian filtering provided a suitable balance between noise reduction and edge preservation and was selected for subsequent processing steps.

---

### 3.2 Contrast Enhancement

Lung ultrasound images typically exhibit low contrast, which can hinder lesion detection. Contrast enhancement techniques, including histogram equalization, were applied to improve the visibility of relevant structures.

These methods enhance intensity differences within the image and facilitate subsequent segmentation and analysis.

---

### 3.3 Ultrasound Region of Interest Extraction

An automatic method was implemented to extract the ultrasound field from the surrounding black background. This step ensures that all further processing is restricted to the clinically relevant region of the image.

The region of interest is identified through contrast enhancement, thresholding, and morphological operations, resulting in a stable contour that delineates the ultrasound field.

---

### 3.4 Lung Lesion Segmentation

#### 3.4.1 Semi-Automatic Segmentation

An experimental semi-automatic segmentation approach combining the Watershed algorithm and Active Contour (Snake) models was implemented. This method requires user-defined markers to guide the segmentation process.

The semi-automatic approach was used to evaluate the influence of guided input on segmentation quality and to identify the limitations of user-dependent methods.

---

#### 3.4.2 Automatic Segmentation Approach

A fully automatic segmentation method was developed to eliminate the need for user interaction. The approach is based on multi-level thresholding (Multi-Otsu), followed by morphological operations and Active Contour refinement.

This method provides consistent lesion segmentation results and represents the final preprocessing solution used in the project.

---

## 4. Feature Extraction and Classification

### 4.1 Feature Extraction

Following automatic lesion segmentation, quantitative image features were extracted from the detected lesion regions. The purpose of this stage is to convert visual information into numerical descriptors suitable for machine learning classification.

A set of features was computed for each segmented lesion and grouped into three main categories:

- **Geometric features:**
  - lesion area;
  - lesion perimeter;
  - circularity index;
  - aspect ratio;

- **Intensity-based features:**
  - mean grayscale intensity within the lesion;
  - standard deviation of intensity values;

- **Structural features:**
  - compactness;
  - solidity;
  - edge density inside the lesion region.

Geometric descriptors provide information regarding lesion shape irregularity, which is commonly associated with malignant formations. Intensity-based features reflect internal heterogeneity, while structural descriptors capture boundary consistency and morphological compactness.

Each segmented lesion is therefore represented as a numerical feature vector that summarizes its morphological and intensity characteristics.

---

### 4.2 Dataset Organization and Preparation for Training

## Dataset Availability

The ultrasound dataset used in this project is not publicly distributed due to medical data privacy considerations.

The dataset used for classification was organized into two separate directories corresponding to the two classes:

- `cancer`
- `non-cancer`

Each directory contains the ultrasound images associated with the respective diagnosis. This folder-based structure enables automatic label assignment during data loading, where the folder name represents the ground truth class.

After segmentation and feature extraction, each processed image is associated with its corresponding class label derived from the directory structure.

The complete feature dataset was then divided into training and testing subsets using a standard train-test split strategy. A ratio of 70% for training and 30% for testing was adopted in order to evaluate model generalization on unseen data.

The split was performed using a fixed random state to ensure reproducibility of the experimental results.

---

### 4.3 Classification Model

A supervised binary classification approach was adopted to distinguish between cancerous and non-cancerous lesions.

Logistic Regression was selected as the classification model due to:

- its simplicity and computational efficiency;
- its interpretability in medical decision-support contexts;
- its suitability for binary classification problems;
- its ability to provide probabilistic outputs.

The model estimates the probability that a lesion belongs to the cancer class based on a linear combination of the extracted features.

Training was performed using the training subset, and the resulting model was evaluated on the independent test subset.

---

### 4.4 Model Evaluation

Model performance was assessed using standard evaluation metrics:

- confusion matrix;
- accuracy;
- precision;
- recall;
- F1-score.

The confusion matrix provides a detailed breakdown of prediction outcomes, including:

- true positives (correctly classified cancer cases);
- true negatives (correctly classified non-cancer cases);
- false positives;
- false negatives.

Accuracy measures overall correctness, while precision and recall provide insight into the balance between false alarms and missed detections. The F1-score provides a harmonic balance between precision and recall.

These metrics allow objective evaluation of the system’s classification capability and support further model refinement.

---

### 4.5 Uncertainty Zone and Decision Thresholding

In addition to standard binary classification, an uncertainty zone was introduced to improve decision reliability.

Instead of using a single fixed probability threshold (e.g., 0.5), two probability thresholds were defined:

- probabilities below a lower threshold are classified as non-cancer;
- probabilities above an upper threshold are classified as cancer;
- probabilities between the two thresholds are labeled as **uncertain**.

This strategy reduces the risk of confident but incorrect predictions and reflects real-world clinical reasoning, where ambiguous cases require additional investigation rather than automatic labeling.

The introduction of an uncertainty zone enhances the safety and practical relevance of the system.

---

### 4.6 System Output

The final system provides:

- segmented lesion visualization;
- extracted feature values;
- predicted class label;
- associated probability score;
- optional uncertainty indication.

By combining visual information with quantitative and probabilistic outputs, the system supports objective and consistent interpretation of lung ultrasound images.

