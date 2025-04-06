# 🔍 Distilling Zero-Shot Knowledge with Minimal Data

This repository provides code and results for our experiments on distilling the zero-shot capabilities of foundation models (like DINOv1/v2) into compact student networks like EfficientNet and TinyViT.

---

## 🧠 Core Idea

We explore how much *zero-shot knowledge* can be distilled from a powerful vision transformer (e.g., DINOv2) into smaller networks with minimal data. The distilled student models are tested on multiple datasets.

---

---

## Setup Env
```
conda env create -f environment.yml
```

## weights
```
# Chestxray dinov1 weights
https://www.kaggle.com/code/ajaymin28/dinoxray-test-acc-95-5/output

# DinoV1 distill to efficientnetB0 weights 
https://www.kaggle.com/code/ajaymin28/dinoxraydistilled
```



## 🧪 Experiments

We distilled knowledge from DINOv1 and DINOv2 into smaller models using **Caltech101** and **ChestXRay** datasets. The distilled models were then evaluated on **Caltech101, CIFAR10, CIFAR100**, and **ChestXRay**.

### 📊 Model Parameters and Latency

| # | Model           | #Param | Latency (s) | Model Size |
|---|----------------|--------|-------------|-------------|
| 1 | DinoV1         | 21M    | 1.05        | 336MB       |
| 2 | DinoV2         | 21M    | 0.31        | 84.1MB      |
| 3 | EfficientNetB0 | 5.3M   | 0.06        | 17.4MB      |
| 4 | EfficientNetV2 | 22M    | 0.004       | 79.7MB      |
| 5 | TinyViT        | 5M     | 0.09        | 47.0MB      |

### 🧪 Zero-Shot Performance (No Distillation)

| Sr No | Dataset    | DINOv1 (R/P)      | DINOv2 (R/P)      |
|-------|------------|-------------------|-------------------|
| 1     | Caltech101 | 96.95 / 86.46     | 98.09 / 89.70     |
| 2     | CIFAR10    | 98.11 / 89.71     | 98.60 / 92.53     |
| 3     | CIFAR100   | 88.81 / 65.73     | 90.85 / 72.28     |
| 4     | ChestXRay  | 92.99 / 80.82     | 91.71 / 78.39     |
| 5     | ChestXRay* | 96.53 / 88.35     | - / -             |

### 📈 Distilled Models Performance


#### Using Caltech101 DINOv1

| Sr No | Dataset    | EfficientB0 (R/P) | EfficientV2 (R/P) | TinyViT (R/P) |
|-------|------------|--------------------|--------------------|----------------|
| 1     | Caltech101 | 60.80 / 37.13      | 6.51 / 1.42        | 91.61 / 82.99  |
| 2     | CIFAR10    | 69.98 / 27.92      | 43.51 / 11.15      | 76.57 / 37.33  |
| 3     | CIFAR100   | 25.24 / 7.26       | 5.64 / 1.14        | 35.83 / 12.66  |
| 4     | ChestXRay  | 94.53 / 56.68      | 89.18 / 52.30      | 94.01 / 63.36  |

#### Using Caltech101 DINOv2

| Sr No | Dataset    | EfficientB0 (R/P) | EfficientV2 (R/P) | TinyViT (R/P) |
|-------|------------|--------------------|--------------------|----------------|
| 1     | Caltech101 | 67.10 / 47.37      | 41.68 / 20.04      | 92.14 / 83.91  |
| 2     | CIFAR10    | 71.39 / 29.97      | 67.53 / 26.22      | 78.69 / 39.64  |
| 3     | CIFAR100   | 29.52 / 9.44       | 21.96 / 6.11       | 37.20 / 14.08  |
| 4     | ChestXRay  | 93.55 / 56.78      | 95.08 / 56.87      | 95.17 / 63.39  |

#### Using ChestXRay DINOv1

| Sr No | Dataset    | EfficientB0 (R/P) | EfficientV2 (R/P) | TinyViT (R/P) |
|-------|------------|--------------------|--------------------|----------------|
| 1     | Caltech101 | 14.28 / 3.92       | 13.01 / 3.52       | 4.34 / 0.91    |
| 2     | CIFAR10    | 59.02 / 19.52      | 55.51 / 16.93      | 41.62 / 10.14  |
| 3     | CIFAR100   | 14.04 / 3.33       | 11.45 / 2.59       | 4.91 / 1.00    |
| 4     | ChestXRay  | *96.03 / *91.53      | *93.63 / *56.78      | *88.89 / *50.69  |

(* Fine-tuned DINOv1 on ChestXRay)



## 🙏 Acknowledgements
- [DINOv2](https://github.com/facebookresearch/dinov2)
- [EfficientNet](https://github.com/google/automl/tree/master/efficientnetv2)
- [TinyViT](https://github.com/microsoft/Cream/tree/main/TinyViT)
