# Agricultural Land Classification using Satellite Imagery

![IBM](https://img.shields.io/badge/IBM-AI%20Developer-054ADA?style=for-the-badge&logo=ibm&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=for-the-badge&logo=keras&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge)

---

## Overview

This is the capstone project for the **IBM AI Developer Professional Certificate**, built around a real-world scenario: an AI Engineer at a fertilizer company tasked with developing an automated land classification system using satellite imagery.

The system classifies terrain types — crops, forests, water bodies, and more — using deep learning models built in both **Keras** and **PyTorch**, with a strong emphasis on comparing CNNs against Vision Transformers.

---

## Problem Statement

Agricultural companies need accurate, scalable land classification to make informed decisions around soil management, crop planning, and resource allocation. Manual analysis of satellite imagery is slow and error-prone. This project automates that process using deep learning on geospatial image datasets.

---

## Project Structure

```
capstone-land-classification/
│
├── Module_1_Data_Handling/
│   ├── memory_vs_generator_loading.ipynb
│   ├── data_augmentation_keras.ipynb
│   ├── data_augmentation_pytorch.ipynb
│   └── custom_geospatial_dataloader.ipynb
│
├── Module_2_CNN_Development/
│   ├── cnn_keras.ipynb
│   ├── cnn_pytorch.ipynb
│   └── performance_evaluation.ipynb
│
├── Module_3_Vision_Transformer/
│   ├── vit_keras_finetuning.ipynb
│   ├── vit_pytorch_finetuning.ipynb
│   └── cnn_vs_vit_comparison.ipynb
│
├── Module_4_Final_Project/
│   ├── comparative_analysis.ipynb
│   └── final_report.pdf
│
├── Data/
└── README.md
```

---

## Modules

### Module 1 — Data Handling

**Objective:** Efficient loading and augmentation of geospatial image datasets.

- Memory-based vs. generator-based data loading strategies
- Image augmentation pipelines using Keras `ImageDataGenerator` and PyTorch `transforms`
- Custom geospatial data loader for model training workflows

---

### Module 2 — CNN Development

**Objective:** Design and train CNN models for multi-class terrain classification.

- CNN architecture built in **Keras** (Sequential + Functional API)
- CNN architecture built in **PyTorch** (nn.Module)
- Performance evaluation using accuracy, precision, and recall
- Framework comparison: Keras vs. PyTorch for image classification tasks

---

### Module 3 — CNN + Vision Transformer Integration

**Objective:** Apply transfer learning with Vision Transformers and benchmark against CNNs.

- Fine-tuning pretrained Vision Transformer (ViT) models in Keras and PyTorch
- Side-by-side comparison of CNN vs. ViT performance on the same dataset
- Analysis of tradeoffs: training time, accuracy, and generalization

---

### Module 4 — Final Project & Wrap-Up

**Objective:** Produce a consolidated, professionally documented solution.

- Full comparative analysis across all models trained
- Final project report covering methodology, results, and insights
- Jupyter notebooks submitted with clarity, technical depth, and reproducibility

---

## Models Built

| Model | Framework | Type |
|---|---|---|
| Custom CNN | Keras | Convolutional Neural Network |
| Custom CNN | PyTorch | Convolutional Neural Network |
| Fine-tuned ViT | Keras | Vision Transformer |
| Fine-tuned ViT | PyTorch | Vision Transformer |

---

## Evaluation Metrics

| Metric | Purpose |
|---|---|
| Accuracy | Overall classification performance |
| Precision & Recall | Per-class reliability |
| F1-Score | Balance between precision and recall |
| AU-ROC | Model discrimination across thresholds |

---

## Tech Stack

```
Languages   : Python 3.10+
Frameworks  : PyTorch, Keras / TensorFlow
Data        : NumPy, Pandas, Matplotlib, Albumentations
Notebooks   : Jupyter, Google Colab
Models      : Custom CNNs, Pretrained Vision Transformers (ViT)
```

---

## Final Outcomes

By the end of this capstone:

- Built and trained CNN and Vision Transformer models for geospatial terrain classification
- Applied transfer learning to improve model accuracy on limited satellite imagery
- Evaluated models using industry-standard metrics (Accuracy, F1, AU-ROC)
- Produced a professional final report documenting methodology and comparative results

---

## Related Repositories

- [Deep Learning & Generative AI — Full Course Repo](https://github.com/adarshadan/DeepLearningAndGenerativeAI)

---

*Part of the IBM AI Developer Professional Certificate — Capstone Project*
