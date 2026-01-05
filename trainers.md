# Gaussian Splatting Trainers – Comparative Table

| Tool Type | Name | Tags | Open Source | Platform | Input | Output Format | Output Size | Processing Time | Entry Guide | Validation | Notes |
|----------|------|------|-------------|----------|-------|---------------|-------------|-----------------|-------------|------------|------|
| Trainer + Viewer | **Luma AI** | trainer, online, commercial, web-view | No | Cloud | Video / Images | Proprietary | Medium | Medium | Easy | Tested by author | Cloud GS pipeline, limited parameter control |
| Trainer + Viewer | **Teleport** | trainer, online, commercial, immersive-view | No | Cloud | Video | Proprietary | Medium | Low | Easy | Tested by author | VR-oriented GS pipeline |
| Trainer + Viewer | **Postshot** | trainer, desktop, commercial, desktop-view | No | Windows | Images / Video | `.ply`, `.splat` | High | Medium | Easy | Tested by author | Local GS training |
| Trainer + Viewer | **Polycam** | trainer, online, mobile, commercial, web-view | No | iOS / Android / Cloud | Video / Images | `.splat` | Medium | Low | Easy | Community-reported, Declared (docs) | Mobile-first GS pipeline |
| Trainer + Viewer | **Scaniverse** | trainer, mobile, commercial, immersive-view | No | iOS | Video | `.splat` | Medium | Low | Easy | Tested by author | On-device GS capture and AR viewing |
| Trainer | **Inria Gaussian Splatting** | trainer, desktop, open-source | Yes | Windows / Linux | Images | `.ply` | Variable | High | Medium | Tested by author | Reference open-source implementation |
| Trainer | **gsplat** | trainer, desktop, open-source | Yes | Linux | Images | `.ply` | Variable | High | Medium | Declared (docs) | Research-oriented framework |
| Trainer | **Scaffold-GS** | trainer, desktop, open-source | Yes | Linux | Images | `.ply` | Medium | Medium | Hard | Declared (docs) | Optimized GS training strategy |
