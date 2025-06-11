# Landmark 3D Reconstruction and AR Visualization

This project implements a full Structure-from-Motion (SfM) pipeline to reconstruct the **Brandenburg Gate** using 2D images, followed by visualization of the reconstructed 3D model in **Augmented Reality (AR)** using a Flutter-based Android application.

## Table of Contents

- [Overview](#overview)
- [3D Reconstruction (SfM)](#3d-reconstruction-sfm)
  - [Dataset Preparation](#dataset-preparation)
  - [Feature Detection & Matching](#feature-detection--matching)
  - [Camera Pose Estimation](#camera-pose-estimation)
  - [3D Triangulation & Visualization](#3d-triangulation--visualization)
- [Augmented Reality Visualization](#augmented-reality-visualization)
  - [App Setup](#app-setup)
  - [Application Workflow](#application-workflow)
- [Results](#results)
  - [Sample SfM Output](#sample-sfm-output)
  - [Sample AR Screenshots](#sample-ar-screenshots)
- [Limitations and Future Work](#limitations-and-future-work)
- [Contributors](#contributors)

---

## Overview

This repository combines traditional 3D reconstruction techniques with mobile AR technology to enable immersive visualizations of historical landmarks. The two core components of this project are:

- **SfM-based 3D reconstruction using OpenCV and Open3D**
- **Mobile AR visualization using Flutter and ARCore**

---

## 3D Reconstruction (SfM)

### Dataset Preparation

1. Use the **Heritage Recon** dataset.
2. Resize and convert all images to grayscale.
3. Select the top 10 images with the most diverse translation values using:
   ```python
   get_top_images_by_translation()
   ```

### Feature Detection & Matching

* Use **ORB** for feature detection.
* Match features using **BFMatcher** with KNN and **Lowe’s ratio test**.
* Apply **RANSAC** to reject outliers.

### Camera Pose Estimation

* Estimate essential matrix using matched keypoints.
* Decompose to retrieve rotation and translation.
* Chain poses relative to the first camera to construct a global frame.

### 3D Triangulation & Visualization

* Perform triangulation to compute 3D points from feature matches.
* Apply cheirality condition to filter valid points.
* Visualize the point cloud using `open3d.visualization.draw_geometries`.

---

## Augmented Reality Visualization (not present in this repository)

### App Setup

* Framework: **Flutter**
* Plugin: `arcore_flutter_plugin` (v0.1.0)
* Device Tested: **Google Pixel 4A**
* Model Format: `.glb` (simplified Brandenburg Gate model)

⚠️ **Note:** The AR plugin is outdated and may require manual fixes for Kotlin compatibility and Google Play Services.

### Application Workflow

```text
1. Start AR session and initialize sensors.
2. Detect flat surfaces using ARCore.
3. User taps a plane to place the model.
4. Load and display the 3D model at the tapped location.
5. Allow user to walk around and inspect the model in 360°.
```

---

## Results

### Sample SfM Output

* Sparse 3D point cloud resembling the Brandenburg Gate.
* Clear distinction of architectural elements like pillars and dome.

### Sample AR Screenshots

* The 3D model appears on real-world planes.
* Allows full navigation around the model for immersive inspection.

---

## Limitations and Future Work

* Limited number of input images with noise impacted accuracy.
* Front-only reconstruction due to narrow camera angles.
* No bundle adjustment performed for optimization.
* Outdated AR plugin introduces build and runtime issues.
* Complex 3D models are hard to load on mid-range phones.
* Heavy dependencies and compatibility conflicts in Flutter.

🔧 **Future Improvements:**

* Integrate bundle adjustment.
* Switch to updated AR libraries (e.g., Sceneform or Unity AR Foundation).
* Use more diverse and cleaner datasets.
* Implement model compression for mobile rendering.

---

## Contributors

* **Muhammad Ahmad Ashraf** – [26100129@lums.edu.pk](mailto:26100129@lums.edu.pk)
* **Sarim Malik** – [26100129@lums.edu.pk](mailto:26100129@lums.edu.pk)

---
