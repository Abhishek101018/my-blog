---
layout: post
title: "📌 GMM-Based Densification of Point Clouds"
date: 2025-04-19
categories: [point-cloud, machine-learning, gmm]
---

Densifying a point cloud can be a tricky job, especially when dealing with sparse datasets captured using LiDAR or photogrammetry. One elegant way to generate more realistic, evenly distributed points is by using **Gaussian Mixture Models (GMM)**!

---

### 🧠 What is GMM?

A **Gaussian Mixture Model** is a probabilistic model that assumes the data is generated from a mixture of several Gaussian distributions. In 3D space, it can help us estimate the distribution of points and generate new ones that **fit the original shape** more smoothly.

---

### 🚀 How GMM Helps in Densification

1. **Fit** a GMM to your sparse point cloud.
2. **Sample** new points from the learned mixture.
3. **Merge** the new points with the original set for a denser cloud.

Simple and elegant!

---

### 🔍 Bonus: Improve Densification Accuracy

You can combine GMM with:

- **Outlier Removal** – to filter noise before fitting
- **Normal Estimation** – for better surface continuity
- **Poisson Sampling** – to redistribute density evenly
- **Graph-based Filtering** – for preserving edges and boundaries

---

### 🧪 Code Example (Python with scikit-learn)

```python
from sklearn.mixture import GaussianMixture
import numpy as np
import open3d as o3d

# Load sparse point cloud
pcd = o3d.io.read_point_cloud("sparse.ply")
points = np.asarray(pcd.points)

# Fit GMM
gmm = GaussianMixture(n_components=10, covariance_type='full')
gmm.fit(points)

# Sample new points
sampled_points, _ = gmm.sample(5000)

# Combine original and sampled
all_points = np.vstack((points, sampled_points))

# Create and save dense cloud
dense_pcd = o3d.geometry.PointCloud()
dense_pcd.points = o3d.utility.Vector3dVector(all_points)
o3d.io.write_point_cloud("dense.ply", dense_pcd)
