# Gaussian Splatting Trainers – Comparative Table

| Tool Type | Name | Tags | Open Source | Platform | Input | Output Format | Output Size | Processing Time | Entry Guide | Notes |
|----------|------|------|-------------|----------|-------|---------------|-------------|-----------------|-------------|------|
| Trainer + Viewer | **Luma AI** | trainer, online, commercial, web-view | No | Cloud | Video / Images | Proprietary, `.ply` (mesh / point cloud export) | Medium | Medium | Easy | Fully automated cloud-based pipeline |
| Trainer + Viewer | **Teleport** | trainer, online, commercial, immersive-view | No | Cloud | Video / Images | Proprietary | Medium | Low | Easy | Desktop and VR-oriented cloud-based pipeline |
| Trainer + Viewer | **Polycam** | trainer, online, mobile, commercial, web-view | No | iOS / Android / Cloud | Video / Images | Multiple 3D formats | Medium | Low | Easy | Mobile and cloud-enabled GS pipeline |
| Trainer + Viewer | **Postshot** | trainer, desktop, commercial, desktop-view | No | Windows | Images / Video | `.ply`, `.spz`, `.psht` | High | Medium | Medium | Local desktop GS training |
| Trainer + Viewer | **Scaniverse** | trainer, mobile, commercial, immersive-view | No | iOS / Android | Video | `.ply`, `.spz` | Medium | Low | Easy | On-device GS capture and VR viewing |
| Trainer | **Inria Gaussian Splatting** | trainer, desktop, open-source | Yes | Windows / Linux | Images | `.ply` | Variable | High | Medium | Reference open-source implementation |
| Trainer | **gsplat** | trainer, desktop, open-source | Yes | Windows / Linux | Images | `.ply` | Variable | High | Medium | High-performance PyTorch library for GS |
| Trainer | **OpenSplat** | trainer, desktop, open-source | Yes | Windows / Linux | Images (COLMAP / Nerfstudio) | `.ply` | Variable | Medium | Medium | C++ native GS implementation based on LibTorch |
| Trainer | **Scaffold-GS** | trainer, desktop, open-source | Yes | Linux | Images | `.ply` | Medium | Medium | Hard | Optimized GS training strategy |



## Notes on the Trainers Table

### Luma AI
- The training pipeline is fully automated and cloud-based. No user-accessible training parameters are exposed.
- Scenes are internally stored as proprietary **Luma Field** assets optimized for real-time rendering.
- Export to standard `.ply` formats (mesh or point cloud) is supported.
- An official **Unreal Engine plugin** is available for real-time visualization of Luma Fields.

### Teleport
- Designed primarily for immersive and VR-oriented visualization.
- Free plan allows up to **5 models**; **`.ply` export** only in paid plan.
- Supports **lightweight (0.25 M)** models for fast previews and **full (~2 M)** models with **LOD** for immersive VR viewing.

### Polycam
- Mobile 3D capture app (iOS/Android) for photogrammetry, LiDAR scans, and 360° captures, with on-device editing and sharing.  
- Cloud/online platform for managing, previewing, editing, and exporting models in formats like GLTF, OBJ, FBX, STL, PLY.  
- Free plan allows limited captures and basic export; paid plans unlock `.splat` export and higher limits.  
- Models can be shared via links, synced across devices, or viewed in community/Poly World feeds.

### Postshot
- Enables local desktop training with configurable reconstruction settings.
- Supports images of any resolution (up to 4K/8K), video inputs, image masking, ACES color space, and geo-referenced data.  
- Can import camera poses/points from 3rd-party tools and focus training on region-of-interest.  
- Models in this work were generated with the **Model Profile Splat3** using **Limit Image Size → 1600px**, **Image Selection → Use Best Images**, **Image Count → 150**, and **Camera poses → Compute From Images**.
- Provides a command-line interface.
- Starting from Postshot v1.0, exporting Gaussian Splatting models in `.ply` format is no longer available under the free license; export options are restricted to paid plans.

### Scaniverse
- Users can explore and interact with splats on mobile and through related VR/WebXR experiences like Into The Scaniverse on Meta Quest.

### Inria Gaussian Splatting
- Reference open-source implementation of Gaussian Splatting introduced in the original research work.
- Provides full control over training parameters, optimization schedule, and data processing.
- Relies on external Structure-from-Motion pipelines (e.g., COLMAP) for camera pose estimation.
- Intended primarily for research, benchmarking, and reproducibility rather than end-user workflows.

### gsplat
- High-performance, open-source library for Gaussian Splatting designed for modular experimentation and research.
- Provides optimized CUDA kernels and supports advanced training strategies, such as **MCMC (Markov Chain Monte Carlo)** densification.
- Built on **PyTorch**, allowing for easy integration with deep learning workflows and custom loss functions.
- Highly efficient in terms of training speed and VRAM management compared to the original reference implementation.

### OpenSplat
- A native **C++ implementation** of Gaussian Splatting based on the **LibTorch** (PyTorch C++ frontend) library.
- Eliminates the need for a Python environment, offering a streamlined, standalone executable for training and processing.
- Closely follows the original Inria optimization pipeline while providing better portability and integration for production software.
- Native support for importing project folders from **COLMAP**, **Nerfstudio**, and **OpenMVG** without additional conversion scripts.

### Scaffold-GS
- Optimized GS training strategy designed to improve structural consistency and rendering quality.
- Focuses on more efficient point distribution and hierarchical structures to handle complex scenes.
