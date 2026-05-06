# 🛰️ LULC Cross-Dataset Generalization with CNNs

A deep learning research project investigating **cross-dataset generalization** of CNN architectures for Land Use and Land Cover (LULC) classification under **domain shift** and **label shift** using satellite imagery.

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-orange)
![Gradio](https://img.shields.io/badge/Demo-Gradio-yellow)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📄 Thesis

This project is the implementation of my undergraduate thesis.

📖 [Read the full thesis](doc/final_thesis_script_v1_1.pdf)

---

## 🔍 Research Overview

Most LULC deep learning studies train and test on the same dataset. This study asks:

> *What happens when a model trained on one satellite dataset is applied to a completely different one?*

We evaluated four ImageNet-pretrained CNN architectures across three regimes:

| Regime | Description |
|--------|-------------|
| **In-Domain** | Train and test on the same dataset |
| **Zero-Shot Transfer** | Apply model directly to a different dataset with no target labels |
| **Few-Shot Fine-Tuning** | Fine-tune with k={5, 10, 20} labeled samples per class |

---

## 📊 Datasets

| Dataset | Classes | Images | Resolution | Sensor |
|---------|---------|--------|------------|--------|
| [EuroSAT](https://github.com/phelber/EuroSAT) | 10 | ~27,000 | 10–60m | Sentinel-2 |
| [UC Merced Land Use](http://weegee.vision.ucmerced.edu/datasets/landuse.html) | 21 | 2,100 | ~1ft | Aerial |

---

## 🧠 Models

- ResNet50
- DenseNet121
- MobileNetV2
- EfficientNetB0

All models use ImageNet pretrained weights with a fine-tuned classification head.

---

## 📈 Key Results

### In-Domain Performance

| Dataset | Best Model | Accuracy | Macro F1 |
|---------|-----------|----------|----------|
| EuroSAT | ResNet50 | 98.50% | 0.9844 |
| UC Merced | ResNet50 | 94.76% | 0.9470 |

### Zero-Shot Cross-Dataset Transfer

Despite strong in-domain performance, **all models collapse under zero-shot transfer**:

| Direction | Best Accuracy |
|-----------|--------------|
| EuroSAT → UC Merced | 7.9% |
| UC Merced → EuroSAT | 11.3% |

### Few-Shot Fine-Tuning (ResNet50)

Even with k=20 labeled samples per class, improvements remain marginal — highlighting the need for explicit domain adaptation methods.

---

## 📁 Repository Structure

```
├── eurosat/               # EuroSAT training notebooks (4 architectures)
│   └── figs/              # Confusion matrices and result plots
├── uc_merced/             # UC Merced training notebooks (4 architectures)
│   └── figs/              # Confusion matrices and result plots
├── cross_dataset/         # Zero-shot and few-shot transfer notebooks
├── comparison/            # Model comparison and ranking notebooks
├── demo/                  # Gradio web demo notebook
└── doc/                   # Thesis PDF
```

---

## 🚀 Running the Notebooks

All notebooks were developed in **Google Colab** with a Tesla T4 GPU.

### Training Notebooks
1. Open any notebook in Google Colab
2. Mount your Google Drive
3. Update the dataset and model save paths
4. Run all cells

### Gradio Demo
The interactive demo loads pretrained models and classifies satellite image patches.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/am-robin11/LULC-cross-dataset-with-CNN/blob/main/demo/final_web_demo.ipynb)

### Pretrained Models
Model weights are stored on Google Drive (too large for GitHub):

📦 [Download Pretrained Models](https://drive.google.com/drive/folders/1oOr8iSfShsO_OCS3pWQxAID9qkkoAKB9?usp=sharing)

After downloading, place files in the appropriate `models/` folder before running notebooks.

---

## 🛠️ Tech Stack

- Python, TensorFlow, Keras
- ResNet50, DenseNet121, MobileNetV2, EfficientNetB0
- NumPy, Matplotlib, Scikit-learn
- Gradio (demo)
- Google Colab (training environment)

---

## 📌 Key Findings

- Models achieving **98%+ in-domain accuracy** can collapse to **single-digit accuracy** under zero-shot cross-dataset transfer
- Transfer is **asymmetric** — UC Merced → EuroSAT performs slightly better than the reverse
- **Few-shot fine-tuning saturates quickly** — simple supervised fine-tuning is insufficient under strong domain and label shift
- Explicit **domain adaptation** methods are needed for reliable real-world LULC deployment

---

## 📄 License

MIT
