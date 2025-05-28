# 🏛️ 3D Landmark Reconstruction and Mobile Visualization
*A Computer Vision Project using SIFT, Triangulation, and Mesh Generation*

This repository presents a complete pipeline for reconstructing 3D landmarks from 2D images using classical computer vision techniques. Developed as part of the **CS436: Computer Vision** course at LUMS, this project culminates in the mobile deployment of the reconstructed 3D model using **FlutterCube**.

> 🧠 **Course**: CS436 - Computer Vision  
> 🗓️ **Semester**: Spring 2025  
> 🏫 **Institution**: LUMS  
> 👨‍💻 Contributors: Muhammad Saad Haroon, Zammad Bin Ziyad Khan

---

## 🧠 Project Overview

The objective is to reconstruct the **Brandenburg Gate** from a set of images using:
- Feature Detection (SIFT)
- Fundamental/Epipolar Geometry
- Camera Pose Estimation
- Linear Triangulation
- Poisson Mesh Generation
- Deployment via FlutterCube (interactive 3D rendering)

![Pipeline](images/pipeline.png "Project Pipeline")

---

## 🎓 Methodology

### 1. 📸 Dataset Preparation
- Dataset: 1400 raw images of the Brandenburg Gate
- Manual filtering to retain 500 relevant views
- Preprocessing: grayscale conversion, histogram equalization

### 2. 🔍 Feature Matching
- SIFT + Brute Force Matcher
- Lowe's Ratio Test
- RANSAC for outlier rejection

### 3. 📷 Camera Estimation
- Extract intrinsics from COLMAP `cameras.bin`
- Compute essential matrix & decompose to poses
- Use `cv2.recoverPose` for rotation & translation

### 4. 🛠️ Triangulation & 3D Points
- Projection matrices for each camera
- 3D point generation via `cv2.triangulatePoints`

### 5. 🧊 Mesh Generation
- Convert to Open3D format
- Compute normals, run Poisson reconstruction
- Output `.obj` model

### 6. 📱 Mobile Deployment
- Use [`flutter_cube`](https://pub.dev/packages/flutter_cube) to render `.obj`
- Implement camera orbit, zoom, and rotate
- Tested on POCO X3 GT (no ARCore)

---

## 🎨 Results

| Module               | Output Quality         |
|----------------------|------------------------|
| Feature Matching     | ✅ 80-100 matches    |
| 3D Triangulation     | ✅ Sparse cloud     |
| Mesh Reconstruction  | ✅ Usable mesh      |
| Mobile App           | ✅ Working UI      |

![Matches](images/2d_matches.png "Matched Keypoints")  
![Mesh](images/3d_mesh_output.png "3D Mesh Output")

---

## 🚨 Challenges & Fixes
- No ARCore device available → fallback to FlutterCube
- Sparse regions in mesh → consider SuperGlue + global match
- Model realism limited → use texture projection in future

---

## 🚀 Future Work
- Switch to dense stereo or MVS for detail
- Use ARCore/Sceneform for real AR
- Add SSIM metrics for quality eval
- Texture mapping

---

## 📖 Citation

If you use this work or find it helpful:

```bibtex
@project{3DLandmarkCV2025,
  title = {3D Landmark Reconstruction and Mobile Visualization},
  note = {Developed as part of CS436: Computer Vision course at LUMS, Spring 2025.}
}
```

---

> “Digitally preserving landmarks is not just about geometry — it’s about bringing heritage to life.”
