# Gaussian Splatting Trainers – Comparative Table

| Tool Type | Name | Tags | Open Source | Platform | Input | Output Format | Output Size | Processing Time | Entry Guide | Notes |
|----------|------|------|-------------|----------|-------|---------------|-------------|-----------------|-------------|------|
| Trainer + Viewer | **Luma AI** | trainer, online, commercial, web-view | No | Cloud | Video / Images | Proprietary, `.ply` (mesh / point cloud export) | Medium | Medium | Easy | Fully automated cloud-based pipeline |
| Trainer + Viewer | **Teleport** | trainer, online, commercial, immersive-view | No | Cloud | Video / Images | Proprietary | Medium | Low | Easy | Desktop and VR-oriented cloud-based pipeline |
| Trainer + Viewer | **Polycam** | trainer, online, mobile, commercial, web-view | No | iOS / Android / Cloud | Video / Images | Multiple 3D formats | Medium | Low | Easy | Mobile and cloud-enabled GS pipeline |
| Trainer + Viewer | **Postshot** | trainer, desktop, commercial, desktop-view | No | Windows | Images / Video | `.ply`, `.splat` | High | Medium | Medium | Local GS training |
| Trainer + Viewer | **Scaniverse** | trainer, mobile, commercial, immersive-view | No | iOS | Video | `.splat` | Medium | Low | Easy | On-device GS capture and AR viewing |
| Trainer | **Inria Gaussian Splatting** | trainer, desktop, open-source | Yes | Windows / Linux | Images | `.ply` | Variable | High | Medium | Reference open-source implementation |
| Trainer | **gsplat** | trainer, desktop, open-source | Yes | Linux | Images | `.ply` | Variable | High | Medium | Research-oriented framework |
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

### Inria Gaussian Splatting
- Reference open-source implementation.
- Provides full control over training parameters.
- Intended primarily for research use.
