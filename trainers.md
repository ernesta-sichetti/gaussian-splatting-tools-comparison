# Gaussian Splatting Trainers – Comparative Table

| Tool Type | Name | Tags | Open Source | Platform | Input | Output Format | Output Size | Processing Time | Entry Guide | Validation | Notes |
|----------|------|------|-------------|----------|-------|---------------|-------------|-----------------|-------------|------------|------|
| Trainer + Viewer | Luma AI | trainer, online, commercial, web-view | 🔴 | Cloud | Video / Images | Proprietary | Medium | Medium | 🟢 | Tested by author | Cloud GS pipeline, limited parameter control |
| Trainer + Viewer | Teleport | trainer, online, commercial, immersive-view | 🔴 | Cloud | Video | Proprietary | Medium | Low | 🟢 | Tested by author | VR-oriented GS pipeline |
| Trainer + Viewer | Postshot | trainer, desktop, commercial, desktop-view | 🔴 | Windows | Images / Video | `.ply`, `.splat` | High | Medium | 🟢 | Tested by author | Local GS training |
| Trainer | Inria Gaussian Splatting | trainer, desktop, open-source | 🟢 | Windows / Linux | Images | `.ply` | Variable | High | 🟡 | Tested by author | Reference open-source implementation |
| Trainer | gsplat | trainer, desktop, open-source | 🟢 | Linux | Images | `.ply` | Variable | High | 🟡 | Declared (docs) | Research-oriented framework |
| Trainer | Scaffold-GS | trainer, desktop, open-source | 🟢 | Linux | Images | `.ply` | Medium | Medium | 🔴 | Declared (docs) | Optimized GS training strategy |
| Trainer + Viewer | Polycam | trainer, online, mobile, commercial, web-view | 🔴 | iOS / Android / Cloud | Video / Images | `.splat` | Medium | Low | 🟢 | Tested by author | Mobile-first GS pipeline |
| Trainer + Viewer | Scaniverse | trainer, mobile, commercial, immersive-view | 🔴 | iOS | Video | `.splat` | Medium | Low | 🟢 | Tested by author | On-device GS capture and AR viewing |
