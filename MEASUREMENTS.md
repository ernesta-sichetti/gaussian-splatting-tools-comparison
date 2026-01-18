# Confronto Gaussian Splatting – Sintesi Visiva

| Tool | Splats | File .ply | Tempo Training | Adatto VR | Note chiave |
|------|--------|-----------|----------------|-----------|------------|
| Nerfstudio | 170k | 43 MB | 30 min | yes | Modello compatto, veloce, ideale per realtime/VR |
| OpenSplat | 273k | 123 MB | 1h | yes | Compromesso ottimale qualità/prestazioni, struttura chiara, stabile in VR |
| gsplat | 1M | 230 MB | 50 min | no* | Modelli densi, artefatti, tempi moderati, non ottimizzato per VR |
| LichtFeld Studio | 1M | 242 MB | 1h | no* | Alta densità, dettagli elevati, sovraccarico GPU in VR |
| Inria GS | 867k | 231 MB | 2h 30m | no* | Riferimento originale, pulito ma pesante |

\* Non ottimizzato per esperienze immersive realtime.

---

## Punti chiave

- **VR / Unity**: OpenSplat è la scelta migliore, bilancia densità e prestazioni.  
- **Efficienza**: Nerfstudio molto leggero e rapido, ma ridotta complessità.  
- **Qualità visiva**: gsplat e LichtFeld Studio producono dettagli elevati ma non sostenibili in VR.  
- **Distribuzione splats**: OpenSplat separa bene struttura e rumore; altri tool mostrano artefatti o floating points.  
- **Scopo della scelta**: ottimizzare **comfort visivo, stabilità e framerate** senza sacrificare troppo dettaglio.

---

**Fonti verificate**:  
- Inria GS – Kerbl et al., SIGGRAPH 2023 ([paper](https://arxiv.org/abs/2308.04079))  
- OpenSplat – [GitHub](https://github.com/pierotofy/OpenSplat)  
- Nerfstudio – [GitHub](https://github.com/nerfstudio-project/nerfstudio)  
- LichtFeld Studio – [sito ufficiale](https://lightfieldlab.com/)  
- Unity VR Best Practices – [Unity Manual](https://docs.unity3d.com/Manual/VRBestPractice.html), [Meta Quest](https://developer.oculus.com/documentation/unity/unity-performance/)# Gaussian Splatting Trainers – Comparative Table

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
The **standard training pipeline** was used for all implementations.  
For **LichtFeld Studio**, the **MCMC-based densification pipeline** was enabled

## 1. Benchmarking Results


| Tool | Output (MB) | # Splats | MB / 100k splats | Train Time | Min / 100k splats |Strategy |
|------|------------:|---------:|----------------:|-----------|-----------------:|--------------------|
| Inria GS | 231 | 955,819 | 24.2 | 150 min | 15.7 | Standard densification |
| gsplat | 230 | 1,000,000 | 23.0 | 50 min | 5.0 | Default densification (CUDA ottimizzato) |
| OpenSplat | 123 | 510,870 | 24.1 | 60 min | 11.7 | Pruning implementazione |
| Nerfstudio | 43 | 170,150 | 25.3 | 30 min | 17.6 | Adaptive culling + gsplat backend |
| LichtFeld Studio | 242 | 1,000,000 | 24.2 | 60 min | 6.0 | Pipeline MCMC (opzionale) |

---

## 2. Technical Overview & Methodologies

### LichtFeld Studio (MCMC Strategy)
LichtFeld implements **3D Gaussian Splatting with Markov Chain Monte Carlo (MCMC)**. This pipeline actively densifies Gaussians in uncertain regions (e.g., textureless walls), producing **1,000,000 splats** in **242 MB** over **1h** of training. This ensures dense coverage of indoor scenes but increases file size.  
* **Source / Info:** [lichtfeld.io](https://lichtfeld.io)

### Inria GS (Original Reference)
The original **Inria** implementation uses **Adaptive Density Control**, relying on gradient-based cloning and splitting. It produces **955,819 splats**, 231 MB, in 2h 30m. Precise but slower than modern optimized backends.  
* **Source / Repo:** [Kerbl et al., SIGGRAPH 2023](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/) | [GitHub](https://github.com/graphdeco-inria/gaussian-splatting)

### gsplat (Optimized Library)
**gsplat** is a PyTorch library with CUDA-optimized rasterization. It maintains the fidelity of the Inria implementation while reducing training time to **50 min**, generating **1,000,000 splats** in 230 MB.  
* **Source / Repo:** [Ye et al., JMLR 2025](https://www.jmlr.org/papers/volume26/24-1476/24-1476.pdf) | [GitHub](https://github.com/nerfstudio-project/gsplat)

### OpenSplat (Native C++)
A portable C++ implementation focused on speed and memory efficiency. Aggressive pruning reduces the number of splats to **510,870**, producing a 123 MB file in 1h.  
* **Source / Repo:** [OpenSplat GitHub](https://github.com/pierotofy/OpenSplat)

### Nerfstudio (Splatfacto)
The **Splatfacto** model uses **adaptive alpha culling** to remove low-contribution Gaussians, producing **170,150 splats** in 43 MB over 30 min. Ideal for high-FPS or VR rendering.  
* **Source / Docs:** [Nerfstudio Documentation](https://docs.nerf.studio/nerfology/methods/splat.html) | [GitHub](https://github.com/nerfstudio-project/nerfstudio)

