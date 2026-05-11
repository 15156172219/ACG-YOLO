# ACG-YOLO

## 📌 Introduction

Internal defect detection in high-pressure aluminum alloy die-cast components is important for industrial quality control and safety assurance. However, industrial X-ray images usually suffer from low defect contrast, blurred boundaries, large morphological variations, and complex background interference. These factors make small, low-contrast, and irregular internal defects difficult to detect accurately.

To address these challenges, we propose **ACG-YOLO**, an adaptive internal defect detection network based on the **YOLOv12** framework. The proposed method is designed for industrial X-ray images of aluminum alloy die-cast components and improves the detection capability for low-contrast, small-scale, and morphologically complex defects.

---

## ✨ Key Contributions

* **DA-C2f Module for Stable Feature Modulation**  
  A DA-C2f module is designed to enhance low-contrast defect features and suppress background noise amplification through multi-level feature aggregation, joint channel–spatial recalibration, and adaptive residual scaling.

* **MSDA-Block and DynDir Module for Structure-Aware Feature Modeling**  
  MSDA-Block and DynDir module are designed to improve the representation of complex internal defects in industrial X-ray images by combining dynamic convolution, multi-scale local modeling, depthwise convolution, and coordinate attention.

* **AdaHead Detection Head for Decoupled Classification and Localization**  
  An adaptive detection head, named AdaHead, is designed to reduce task interference between classification and localization. The regression branch is kept stable, while lightweight attention enhancement is applied only to the classification branch.

---

## 📊 Experimental Results

### Results on the GDXray Dataset

Experimental results on the **GDXray** dataset show that ACG-YOLO achieves a favorable balance between detection accuracy and inference efficiency.

| Model | mAP50 (%) ↑ | mAP50-95 (%) ↑ | Recall (%) ↑ | Precision (%) ↑ | FPS ↑ | Params (M) ↓ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| YOLOv8 | 89.40 | 58.10 | 79.10 | 92.40 | 507 | 3.01 |
| YOLOv10 | 90.00 | 58.60 | 80.10 | 89.70 | 978 | 2.69 |
| YOLO11 | 91.60 | 58.50 | 82.90 | 91.40 | 706 | 2.58 |
| YOLOv12 | 87.90 | 55.30 | 77.50 | 90.90 | 578 | 2.51 |
| YOLOv13 | 88.80 | 56.60 | 80.10 | 90.80 | 515 | 2.45 |
| YOLO26 | 90.10 | 57.90 | 80.80 | 87.80 | 720 | 2.38 |
| RT-DETR | 88.50 | 55.00 | 77.20 | 92.00 | 63 | 76.96 |
| **ACG-YOLO (Ours)** | **93.30** | **59.90** | **84.70** | **93.60** | 742 | 2.57 |

---

### Cross-Dataset Validation on the Al-Cast Dataset

To further evaluate the adaptability of ACG-YOLO on an independent external dataset, supplementary experiments were conducted on the **Al-Cast** dataset.

| Model | Class | mAP50 (%) ↑ | mAP50-95 (%) ↑ | Recall (%) ↑ | Precision (%) ↑ |
| :--- | :---: | :---: | :---: | :---: | :---: |
| YOLOv8 | All | 97.6 | 53.4 | 96.1 | 98.3 |
| YOLOv10 | All | 97.5 | 53.6 | 93.6 | 97.1 |
| YOLO11 | All | 97.8 | 53.4 | 95.9 | 97.7 |
| YOLOv12 | All | 96.9 | 51.8 | 93.9 | 96.2 |
| YOLOv13 | All | 97.1 | 52.2 | 94.5 | 97.2 |
| YOLO26 | All | 97.9 | 51.6 | 96.7 | 97.5 |
| **ACG-YOLO (Ours)** | **All** | **98.5** | **53.7** | 95.6 | 95.3 |
| **ACG-YOLO (Ours)** | **Shrinkage** | **97.9** | **52.8** | 95.0 | 94.2 |
| **ACG-YOLO (Ours)** | **Gas hole** | **99.0** | 54.6 | 96.2 | 96.5 |

---

## 🗂️ Datasets

### GDXray Dataset

The **GDXray** dataset is a public industrial X-ray nondestructive testing database. In this study, the casting subset was used. It contains 2,727 images from 67 sequences, covering different aluminum castings such as wheel hubs and steering knuckles.

### Al-Cast Dataset

The **Al-Cast** dataset was used as an independent external dataset for supplementary validation. It contains X-ray images of high-pressure die-cast components and focuses mainly on two types of internal defects: **shrinkage** and **gas holes**.

---

## ⚙️ Environment Setup

The experiments were conducted under the following environment:

* Deep Learning Framework: PyTorch
* Detection Framework: Ultralytics YOLO
* GPU: NVIDIA RTX 3090D with 24 GB memory
* Python: 3.10
* CUDA: 12.1

---

## 🧪 Training Settings

The main training settings are listed below:

* Input Resolution: 640 × 640
* Epochs: 300
* Batch Size: 32
* Optimizer: SGD
* Initial Learning Rate: 0.01
* Momentum: 0.937
* Dataset Split: 7:2:1 for training, validation, and testing

---

## 📈 Usage

### Training

```python
from ultralytics import YOLO

# Load ACG-YOLO model configuration
model = YOLO("ultralytics/cfg/models/v12/ACG-YOLO.yaml")

# Start training
model.train(
    data="your_dataset.yaml",
    epochs=300,
    imgsz=640,
    batch=32,
    optimizer="SGD",
    lr0=0.01,
    momentum=0.937
)
