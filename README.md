# mixar-3d-mesh-normalization
# 🧊 3D Mesh Pipeline: Min–Max vs Unit Sphere Normalization

### A Comparative Study on Mesh Normalization, Quantization & Reconstruction Error  
**Author:** 🇮🇳 *Nithin Sai*  
**Repository:** `mixar-3d-mesh-normalization`

---

## 📌 Overview

This project implements a **3D mesh preprocessing pipeline** to evaluate two different normalization techniques used in graphics, XR, gaming, and 3D content optimization workflows:

| Method | Description | Pros | Cons |
|--------|----------------|--------|--------|
| **Min–Max Normalization** | Scales mesh coordinates to [0,1] using axis-wise min/max | Best reconstruction accuracy | Less robust to scale variance |
| **Unit Sphere Normalization** | Centers mesh and scales to fit a unit sphere | Scale-invariant & widely used in ML/XR | Slightly higher quantization error |

After normalization, meshes are **quantized to 1024 bins**, then **reconstructed**, and **reconstruction error** is computed to compare both methods.

---

## 🧠 Objectives

✔ Normalize 3D meshes using **Min–Max** and **Unit Sphere**  
✔ Quantize → Dequantize to simulate compression  
✔ Compute reconstruction quality using **MSE and MAE**  
✔ Compare both methods across 5 meshes  
✔ Provide rendered visual comparison sheets  

---

## 🚀 Tech Stack

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![NumPy](https://img.shields.io/badge/NumPy-2.0+-013243.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange.svg)
![Trimesh](https://img.shields.io/badge/Trimesh-Mesh%20Processing-green.svg)
![Blender](https://img.shields.io/badge/Blender-3D%20Rendering-orange.svg)

---

## 📂 Folder Structure

mixar-3d-mesh-normalization
│
├── data/ # Input mesh files (.obj)
├── src/
│ ├── io_utils.py # I/O + stats utility functions
│ ├── normalization.py # Min–Max + Unit Sphere methods
│ ├── quantization.py # Quantize + Dequantize logic
│ ├── error_metrics.py # MSE + MAE calculations
│ └── pipeline.py # Task 1–3 runner for one mesh
│
├── outputs/
│ ├── normalized/ # Normalized meshes
│ ├── quantized/ # Quantized meshes
│ ├── reconstructed/ # Dequantized/reconstructed
│ ├── plots/ # Stats + error plots + JSON
│ └── renders/
│ └── montages/ # Comparison sheets
│
├── blender/
│ ├── render_all.py # Render 4 views per mesh
│ └── make_montage.py # Creates comparison sheets
│
├── run_all.py # Runs Tasks 1–3 for ALL meshes
└── requirements.txt

---

## ✅ Tasks & Implementation

### **📍 Task 1: Mesh Statistics**
Extract vertex statistics for each mesh:

- Vertex count
- Min / Max
- Mean
- Standard deviation

```bash
python src/pipeline.py --mesh data/cube.obj --task 1
