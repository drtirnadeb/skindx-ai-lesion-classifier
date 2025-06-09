# 🧠 SkinDx AI – Skin Lesion Risk Classifier

**SkinDx AI** is an end-to-end deep learning pipeline to classify skin lesions as *benign* or *malignant*, designed to support triage and early risk detection in dermatology. It also includes a public Gradio-based app that allows real-time user interaction.

[🚀 Try the demo](https://huggingface.co/spaces/tirnadebphd/SkinDx-App)

---

## 🗂️ Project Structure

- **SkinDx_App.ipynb**: Full end-to-end notebook with model development, evaluation, and deployment.
- **README.md**: Overview and documentation.
- **Demo (optional)**: [Insert `demo.gif` if available]

---

## 📦 Features

- Binary classification of skin lesions using CNN
- Stratified train-validation-test splits
- Class imbalance handling via weighted loss
- Data augmentation for better generalization
- Comparison of 10+ model variants (CNN, MobileNetV2, EfficientNetB0)
- Triage classifier for 3-class risk stratification (low/moderate/high)
- Tabular modeling with LightGBM/XGBoost
- Meta-ensemble using CNN + tabular models
- Deployed interactive app via Gradio (on Hugging Face Spaces)

---

## 🔍 Dataset

> Skin lesion images with metadata from ISIC or similar public datasets.  
The images were pre-labeled as **benign** or **malignant**, and were resized to `224x224`.

📌 Note: The dataset is not included in the repo due to size and licensing. You can integrate your own by following instructions in the notebook.

---

## 📊 Models Trained

| Model Version                       | Validation Accuracy | Notes |
|------------------------------------|----------------------|-------|
| Baseline CNN                       | ~74%                 | No augmentation or weighting |
| CNN + Data Augmentation            | ~78% ✅              | Best performing binary model |
| CNN + ELU                          | ~63%                 | Underfit |
| CNN + BatchNorm                    | ~37%                 | Poor convergence |
| CNN + Larger Batch Size (64)       | ~73%                 | Stable generalization |
| CNN + Class Weights                | ~76%                 | Improved minority class recall |
| CNN + Aug + Class Weights ✅       | **~78% (Best)**      | Strong generalization |
| MobileNetV2 (binary)               | ~67%                 | Frozen base |
| MobileNetV2 (triage)               | ~76%                 | 3-class softmax |
| EfficientNetB0 (triage)            | ~55%                 | Underperforms (frozen base) |
| Ensemble (CNN + Tabular)           | ~78%                 | Slight boost in F1, ROC-AUC |

---

## 📈 Visualizations

- Training/Validation Accuracy & Loss Curves
- Confusion Matrix
- Classification Reports
- ROC-AUC and Precision-Recall Curves
- Ensemble evaluation using meta-model

---

## 🤖 Deployment

Deployed using Gradio on Hugging Face Spaces:
- Upload an image
- Get binary (benign vs malignant) prediction
- Built as a prototype for accessible image-driven diagnostic tools

[🔗 Access the app here](https://huggingface.co/spaces/tirnadebphd/SkinDx-App)

---

## 💡 Key Learnings

- Data augmentation + class weighting significantly improve generalization on small imbalanced datasets.
- Pretrained models (MobileNetV2, EfficientNetB0) require fine-tuning to outperform custom CNNs.
- Validation accuracy > training accuracy is not necessarily overfitting if dropout and augmentation are applied only during training.
- Combining image and tabular signals helps, but only marginally in this dataset.



---

## 📜 License

MIT License – please credit if you use or adapt this work.
