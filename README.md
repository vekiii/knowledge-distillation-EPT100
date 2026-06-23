# Knowledge Distillation: Optimization on the EPT100 Dataset

This project explores the theory and application of Knowledge Distillation (KD) to optimize and compress neural networks.
It consists of two parts: a theoretical part (seminar paper) and the practical part (Jupyter notebook).
***For now, the project only represents the response-based KD notebook and its report. The rest is in progress.***

## 🚀 Project Overview

The primary objective was to transfer knowledge from a robust, complex model (Teacher) to smaller, computationally efficient models (Students), enabling high accuracy alongside dramatically faster inference on both CPU and GPU hardware.
Experiments were conducted on the **EPT100** dataset (microscopic insect images), analyzing the trade-offs between accuracy, inference speed (latency), and model interpretability.

### Model Architectures:
* **Teacher:** `EfficientNet-B2` (trained on original image resolution - 512x512)
* **Students:** `EfficientNet-B0`, `MobileNetV3`, and a custom miniature architecture `TinyCustom Net`.

---

## 📊 Key Results

### 1. Compactness and Inference Speed
The optimal balance between performance and speed was achieved by **TinyCustomNet KD (T=10)**:
* **Accuracy:** Successfully surpassed the 90% threshold, reaching **91.38%**.
* **GPU Speedup:** **8.16x faster** than `EfficientNet-B0 KD` and **12.22x faster** than the teacher.
* **CPU Speedup:** **8.31x faster** than `EfficientNet-B0 KD` and **93.68x faster** than the teacher, making it ideal for resource-constrained Edge deployment.

### 2. Error Analysis and Calibration
* **Regularization:** Models trained via distillation exhibit significantly lower and healthier confidence levels when making errors compared to rigid models trained strictly on hard labels (HL).
* **Distillation Effect:** In successful configurations (such as `EfficientNet-B0` at T=10), the student successfully inherits the specific decision boundaries of the teacher, adopting its fine systematic errors.
* **Data Noise:** A "hard core" of 22 images was identified that no model (including the teacher) could correctly classify, indicating the presence of objective noise (mislabeled samples) within the EPT100 dataset.

### 3. Interpretability (Grad-CAM)
Visualization using the Grad-CAM method confirmed that baseline HL models often suffer from scattered focus, allocating attention to irrelevant background elements. By increasing the distillation temperature to T=10, the student models (most notably `Tiny CNN`) successfully redirect their focus along the entire body of the insect, closely approximating the teacher's attention maps.

---

## 📁 Repository Structure

* `knowledge_distillation_EPT100.ipynb` - Jupyter Notebook containing the complete pipeline for training, distillation, and evaluation.
* `izvestaj.pdf` - The complete research paper/thesis containing detailed theoretical background and analysis. **(SERBIAN VERSION)**
* `README.md` - Project overview (this file).

> ⚠️ **Note on Model Weights:** Due to GitHub file size restrictions, the complete network weights in the `knowledge_distillation_EPT100` folder are hosted on Hugging Face.

---

## 📦 Downloading Model Weights (Hugging Face)

All trained model weights (Baseline HL, KD T=3, KD T=10) can be downloaded from the Hugging Face repository:

🔗 **[LINK TO HUGGING FACE REPOSITORY](insert_your_hf_link_here)**

To run the models, open the Jupyter notebook file and follow the steps. The project was done in Google Colab, so it contains a specific setup.

---

## 🛠️ NOTE
As I do NOT own the dataset rights, I am not able to publish it publicly.
