# ACG-YOLO
Official PyTorch implementation of ACG-YOLO for aluminum casting internal defect detection using an improved YOLO model.

# Overview
<img width="1467" height="1145" alt="image" src="https://github.com/user-attachments/assets/09d96eb6-e50f-4d55-af64-857026e51a9f" />
The full implementation will be released after the associated paper is accepted.

# Innovations
1.Stable feature enhancement：A DA-C2f module is designed to enhance low-contrast defect features and suppress background noise amplification through multi-level feature aggregation, channel–spatial recalibration, and adaptive residual scaling.

2.Multi-scale directional structure modeling：MSDA-Block and DynDir are developed by combining dynamic convolution, multi-scale local modeling, and coordinate attention to improve the representation of small, elongated, and irregular defects.

3.Classification–localization decoupled head：An AdaHead detection head is designed to enhance only the classification branch while preserving the regression branch, thereby reducing task interference between classification and localization.

# Main Results
| Method | mAP50↑ |	mAP50-95↑	| Re↑	| Pr↑ |	FPS↑ | Params(M)↓ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| YOLOv12 |	87.90 |	55.30 |	77.50 | 90.90 |	578 |	2.51 |
| YOLOv13 |	88.80 | 56.60 | 80.10 | 90.80 | 515 | 2.45 |
| YOLO26 |	90.10 | 57.90 | 80.80 | 87.80 | 720 | 2.38 |
| RT-DETR |	88.50 | 55.00 | 77.20 | 92.00 | 63 | 76.96 |
| ACG-YOLO | 93.30 | 59.90 | 84.70 | 93.60 | 742 | 2.57 |
