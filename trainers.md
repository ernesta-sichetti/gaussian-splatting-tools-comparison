# Gaussian Splatting Trainers – Comparative Table

| Tool Type | Name | Tags | Open Source | Platform | Input | Output Format | Output Size | Processing Time | Entry Guide | Validation | Notes |
|----------|------|------|-------------|----------|-------|---------------|-------------|-----------------|-------------|------------|------|
| Trainer + Viewer | **Luma AI** | trainer, online, commercial, web-view | No | Cloud | Video / Images | Proprietary, `.ply` (mesh / point cloud export) | Medium | Medium | Easy | Tested by author | Fully automated cloud pipeline |
| Trainer + Viewer | **Teleport** | trainer, online, commercial, immersive-view | No | Cloud | Video | Proprietary | Medium | Low | Easy | Tested by author | VR-oriented GS pipeline |
| Trainer + Viewer | **Postshot** | trainer, desktop, commercial, desktop-view | No | Windows | Images / Video | `.ply`, `.splat` | High | Medium | Easy | Tested by author | Local GS training |
| Trainer + Viewer | **Polycam** | trainer, online, mobile, commercial, web-view | No | iOS / Android / Cloud | Video / Images | `.splat` | Medium | Low | Easy | Community-reported, Declared (docs) | Mobile-first GS pipeline |
| Trainer + Viewer | **Scaniverse** | trainer, mobile, commercial, immersive-view | No | iOS | Video | `.splat` | Medium | Low | Easy | Tested by author | On-device GS capture and AR viewing |
| Trainer | **Inria Gaussian Splatting** | trainer, desktop, open-source | Yes | Windows / Linux | Images | `.ply` | Variable | High | Medium | Tested by author | Reference open-source implementation |
| Trainer | **gsplat** | trainer, desktop, open-source | Yes | Linux | Images | `.ply` | Variable | High | Medium | Declared (docs) | Research-oriented framework |
| Trainer | **Scaffold-GS** | trainer, desktop, open-source | Yes | Linux | Images | `.ply` | Medium | Medium | Hard | Declared (docs) | Optimized GS training strategy |

## Notes on the Trainers Table

### Luma AI
- The training pipeline is fully automated and cloud-based. No user-accessible training parameters are exposed.
- Scenes are internally stored as proprietary **Luma Field** assets optimized for real-time rendering.
- Export to standard `.ply` formats (mesh or point cloud) is supported.
- An official **Unreal Engine plugin** is available for real-time visualization of Luma Fields.

### Teleport
- Designed primarily for immersive and VR-oriented visualization.
- Emphasis is placed on ease of use rather than parameter control.

### Postshot
- Allows local desktop training with partial control over reconstruction settings.
- Supports standard Gaussian Splatting export formats.

### Inria Gaussian Splatting
- Reference open-source implementation.
- Provides full control over training parameters.
- Intended primarily for research use.
