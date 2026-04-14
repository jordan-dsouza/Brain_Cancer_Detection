---

# Brain Cancer Detection using CNN and Transfer Learning

## Overview

This project focuses on the classification of brain MRI images into multiple cancer categories using deep learning techniques. The dataset used is the **Orvile Brain Cancer MRI Dataset** sourced from Kaggle and directly integrated into the workflow using the Kaggle API in Google Colab.

The dataset consists of three classes:

* **Glioma**
* **Meningioma**
* **Tumor**

The primary objective is to develop a robust convolutional neural network (CNN) model and benchmark its performance against a pretrained **MobileNetV2** architecture.

---

## Dataset & Preprocessing

* All images are in **grayscale format** with an original resolution of **512×512**.
* Images were resized to **128×128** to reduce computational complexity.
* Pixel values were normalized to the range **[0, 1]**.
* Labels were encoded as:

  * Glioma -> 0
  * Meningioma -> 1
  * Tumor -> 2

The dataset was split into:

* **80% Training set**
* **20% Test set**

A **stratified split** was used to preserve class distribution across training and testing sets.

---

## Methodology

### Custom CNN Architecture

A sequential convolutional neural network was designed with the following components:

* **Input Layer:** Shape (128, 128, 1)
* **Convolutional Layers:**

  * Two Conv2D layers with 32 and 64 filters respectively to extract hierarchical spatial features
* **Batch Normalization:**

  * Applied after each convolutional layer to stabilize training and accelerate convergence
* **Max Pooling Layers:**

  * Downsampling using 2×2 filters to reduce spatial dimensions while preserving key features
* **Dropout Layers:**

  * Applied with rates of 0.3 (input) and 0.5 (dense layers) to mitigate overfitting
* **Flatten Layer:**

  * Converts feature maps into a 1D vector
* **Fully Connected (Dense) Layer:**

  * Learns complex feature interactions prior to classification

---

## Model Configuration

* **Optimizer:** Adam (adaptive learning rate optimization)
* **Loss Function:** Sparse Categorical Crossentropy
* **Evaluation Metric:** Accuracy

---

## Training Strategy

* **Epochs:** 10
* **Batch Size:** 32
* **Early Stopping:**

  * Training halted if validation loss did not improve for 3 consecutive epochs
* **Training Time:** ~33 minutes

Early stopping was employed as a regularization strategy to prevent overfitting and improve generalization.

---

## Results

### Custom CNN Model

* **Test Accuracy:** 78.47%

Training and validation performance were monitored using:

* Accuracy vs Epochs
* Loss vs Epochs

---

## Transfer Learning with MobileNetV2

To improve performance, a pretrained **MobileNetV2** model was utilized.

### Key Adjustments:

* Input reshaped to **(128, 128, 3)** to match RGB requirements
* Grayscale images converted to 3-channel format
* Base model layers were **frozen** to leverage pretrained feature representations
* Classification head trained on the target dataset

### Performance:

* **Test Accuracy:** 94.06%

This demonstrates the effectiveness of transfer learning in achieving higher accuracy with reduced training effort.

---

## Discussion & Future Improvements

Several strategies were identified to further enhance model performance:

1. **Model Architecture Optimization**

   * Increasing depth (additional Conv/Dense layers)
   * Fine-tuning dropout and normalization strategies

2. **Higher Resolution Input**

   * Using **224×224** images to retain more spatial detail

3. **K-Fold Cross Validation**

   * More robust evaluation and hyperparameter tuning
   * Trade-off: increased computational cost

4. **Fine-Tuning Pretrained Models**

   * Unfreezing deeper layers of MobileNetV2 for domain-specific learning

---

## Conclusion

This project demonstrates:

* The effectiveness of CNNs for medical image classification
* The significant performance gains achieved through **transfer learning**
* Practical trade-offs between computational efficiency and model accuracy

The MobileNetV2-based approach substantially outperformed the custom CNN, highlighting the importance of leveraging pretrained architectures in real-world deep learning applications.

---

