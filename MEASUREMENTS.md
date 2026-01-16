# Gaussian Splatting Trainers – Comparative Table

| Name | Tool Type | Tags | Platform | Processing Time | Output Size | Notes |
|:-----|:----------|:-----|:---------|:---------------:|:-----------:|:------|
| **Luma AI** | Trainer + Viewer | online, commercial | Cloud | 45 min | ~200 MB | Fully automated cloud-based pipeline |
| **Teleport** | Trainer + Viewer | online, commercial | Cloud | 50 min | 56 - 463 MB | Two quality tiers (Standard/High) |
| **Postshot** | Trainer + Viewer | desktop, commercial | Windows | 1h | ~250 MB | High-quality MCMC-based training |
| **Inria GS** | Trainer | desktop, open-source | Win / Linux | 2h 30m | 231 MB | Original reference implementation |
| **gsplat** | Trainer | open-source, library | Win / Linux | 50 min | 230 MB | High-performance PyTorch backend |
| **OpenSplat** | Trainer | open-source, implementation | Win / Linux | 1h | 123 MB | Efficient C++ native implementation |
| **Nerfstudio** | Trainer + Viewer | open-source, framework | Win / Linux | 30 min | 43 MB* | Modular framework (Fast/Low density) |
| **LichtFeld Studio** | Trainer + Viewer | open-source, implementation | Windows | 1h | **242 MB** | Optimized MCMC training for interiors |

# 3D Gaussian Splatting: Software Benchmark & Technical Analysis

This study compares five major implementations of **3D Gaussian Splatting (3DGS)** using a standardized indoor dataset of **150 images** and a fixed training budget of **30,000 iterations** on an **NVIDIA RTX 4060**.

## 1. Benchmarking Results

| Implementation | Type | Output Size | Points (Est.) | Train Time | Strategy |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **LichtFeld Studio** | C++/CUDA | **242 MB** | ~1.1M | 1h 00m | **MCMC Densification** |
| **Inria GS** | Reference | **231 MB** | ~1.0M | 2h 30m | **Adaptive Density Control** |
| **gsplat** | Library | **230 MB** | ~1.0M | 50m | Optimized CUDA Kernels |
| **OpenSplat** | C++/Lean | **123 MB** | ~500k | 1h 00m | Balanced Pruning |
| **Nerfstudio** | Framework | **41 MB** | **170,150** | 30m | **Adaptive Alpha Culling** |

---

## 2. Technical Overview & Methodologies

### LichtFeld Studio (MCMC Strategy)
LichtFeld implements **3D Gaussian Splatting as Markov Chain Monte Carlo (MCMC)**. Unlike standard heuristics, this method treats Gaussians as samples from a probability distribution. It actively populates "uncertain" areas (e.g., textureless white walls), which significantly increases point density and file size but ensures superior surface coverage for indoor scenes.
* **Source:** [Kheradmand et al., "3D Gaussian Splatting as Markov Chain Monte Carlo", NeurIPS 2024](https://arxiv.org/abs/2404.09591).

### Inria GS (Original Reference)
The original implementation from **Inria** introduced **Adaptive Density Control**. It relies on gradient-based cloning and splitting. While precise, its training speed is limited by 2023-era CUDA kernels compared to modern optimized backends.
* **Source:** [Kerbl et al., "3D Gaussian Splatting for Real-Time Radiance Field Rendering", SIGGRAPH 2023](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/).

### gsplat (Optimized Library)
Developed by the Nerfstudio team, **gsplat** is a highly optimized library for PyTorch. It provides a significant speedup (50m vs 2h30m) by utilizing custom CUDA kernels for the forward and backward rasterization passes while maintaining the fidelity of the original Inria implementation.
* **Source:** [Ye et al., "gsplat: An Open-Source Library for Gaussian Splatting", JMLR 2025](https://www.jmlr.org/papers/volume26/24-1476/24-1476.pdf).

### OpenSplat (Native C++)
A portable, lean implementation written in **C++**. It focuses on performance and memory efficiency. The reduced output size (123 MB) is a result of more aggressive "pruning" during training, which discards Gaussians with low visual contribution to optimize for faster inference.
* **Source:** [OpenSplat Repository](https://github.com/pierotofy/OpenSplat).

### Nerfstudio (Splatfacto)
The **Splatfacto** model within Nerfstudio is designed for efficiency and developer-friendliness. The small file size (**41 MB**) is primarily due to an **Alpha Cull Threshold** that aggressively removes translucent Gaussians. This makes the models ideal for high-FPS rendering in VR environments.
* **Source:** [Nerfstudio Documentation - Splatfacto Model](https://docs.nerf.studio/nerfology/methods/splat.html).

---

## References
* Kerbl, B., et al. (2023). "3D Gaussian Splatting for Real-Time Radiance Field Rendering". *ACM Transactions on Graphics*.
* Kheradmand, S., et al. (2024). "3D Gaussian Splatting as Markov Chain Monte Carlo". *NeurIPS*.
* Ye, V., et al. (2025). "gsplat: An Open-Source Library for Gaussian Splatting". *JMLR*.
