# mixar-3d-mesh-normalization
# 🧊 3D Mesh Pipeline: Min–Max vs Unit Sphere Normalization

### A Comparative Study on Mesh Normalization, Quantization & Reconstruction Error  
**Author:** 🇮🇳 *Nithin Sai*  
**Repository:** `mixar-3d-mesh-normalization`

📌 Overview

This project implements a **3D mesh preprocessing pipeline** to evaluate two different normalization techniques used in graphics, XR, gaming, and 3D content optimization workflows:

| Method | Description | Pros | Cons |
|--------|----------------|--------|--------|
| **Min–Max Normalization** | Scales mesh coordinates to [0,1] using axis-wise min/max | Best reconstruction accuracy | Less robust to scale variance |
| **Unit Sphere Normalization** | Centers mesh and scales to fit a unit sphere | Scale-invariant & widely used in ML/XR | Slightly higher quantization error |

After normalization, meshes are **quantized to 1024 bins**, then **reconstructed**, and **reconstruction error** is computed to compare both methods.


🧠 Objectives

✔ Normalize 3D meshes using **Min–Max** and **Unit Sphere**  
✔ Quantize → Dequantize to simulate compression  
✔ Compute reconstruction quality using **MSE and MAE**  
✔ Compare both methods across 5 meshes  
✔ Provide rendered visual comparison sheets  



🚀 Tech Stack

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![NumPy](https://img.shields.io/badge/NumPy-2.0+-013243.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange.svg)
![Trimesh](https://img.shields.io/badge/Trimesh-Mesh%20Processing-green.svg)
![Blender](https://img.shields.io/badge/Blender-3D%20Rendering-orange.svg)



📂 Folder Structure

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



✅ Tasks & Implementation

📍 Task 1: Mesh Statistics**
Extract vertex statistics for each mesh:

- Vertex count
- Min / Max
- Mean
- Standard deviation

python src/pipeline.py --mesh data/cube.obj --task 1

📍Task 2: Normalization + Quantization

Runs Min–Max and Unit Sphere normalization → Quantization (1024 bins)

python src/pipeline.py --mesh data/cube.obj --task 2 --method minmax --bins 1024
python src/pipeline.py --mesh data/cube.obj --task 2 --method unit_sphere --bins 1024

📍 Task 3: Reconstruction + Error Metrics

Computes reconstruction error after dequantization:

python src/pipeline.py --mesh data/cube.obj --task 3 --method minmax --bins 1024
python src/pipeline.py --mesh data/cube.obj --task 3 --method unit_sphere --bins 1024


Outputs include:

MSE

MAE

Per-axis errors

JSON + Plot

🚀 Run Complete Pipeline on All Meshes
python run_all.py --bins 1024

🎨 Visual Comparison (Min–Max)

Below are the comparison sheets for the Min–Max pipeline:

📍 Add your images here after uploading to GitHub (drag & drop):

Example placeholder (replace with your images):

outputs/renders/montages/comparison_cube.png
outputs/renders/montages/comparison_sphere.png
outputs/renders/montages/comparison_torus.png
outputs/renders/montages/comparison_cylinder.png
outputs/renders/montages/comparison_cone.png

📊 Results Summary
🔥 Reconstruction Error (1024 bins)
Mesh	Min–Max MSE	Unit Sphere MSE	Winner
Cube	0.00	4.00e-06	Min–Max
Cylinder	7.81e-07	3.08e-06	Min–Max
Cone	7.83e-07	2.54e-06	Min–Max
Sphere	1.25e-06	1.25e-06	Tie
Torus	2.50e-06	3.62e-06	Min–Max
🧠 Key Insights

Min–Max preserved geometry better across 4/5 meshes

Sphere tied because radial symmetry suits unit-sphere scaling

Unit Sphere is more robust across arbitrary scales, but slightly lossy after quantization

For XR pipelines requiring accuracy, Min–Max is recommended

For applications needing scale-invariance, Unit Sphere is preferred

🖥️ Rendering with Blender

Generate renders of Original → Normalized → Quantized → Reconstructed

Run Blender Renders
"C:\Program Files\Blender Foundation\Blender 3.6\blender.exe" -b -P blender/render_all.py

 Build comparison sheets
python blender/make_montage.py

🧪 Future Improvements

Visual comparison for Unit Sphere pipeline

Add rotation-invariant normalization

Add mesh topology metrics

Support more formats (.fbx, .stl, .gltf)

✨ Author

🇮🇳 Nithin Sai

If this repo helped you or you found the comparison insightful, ⭐ star the repository!



