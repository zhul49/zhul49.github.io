---
layout: post
modal-id: 5
date: 2025-01-18
featured: true
title: EKF SLAM on Turtlebot3
subtitle: Building a full SLAM stack from scratch
img: output.mp4
alt: EKF SLAM on TurtleBot3
project-date: Mar 2026
description: "A TurtleBot3 that maps its environment and localizes itself in real time using EKF SLAM, built from scratch in ROS 2."
tags:
  - ROS 2
  - C++
  - Unsupervised Learning
  - SLAM
  - EKF
  - TurtleBot3
github: https://github.com/zhul49/slam-zhul49
---

## Demo

<div style="text-align: center; margin: 20px 0;">
  <video class="img-responsive img-centered" autoplay loop muted playsinline style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <source src="{{ site.url }}/img/portfolio/Closed_loop_run.mp4" type="video/mp4">
  </video>
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">Red = ground truth &nbsp;·&nbsp; Blue = odometry &nbsp;·&nbsp; Green = SLAM estimate and landmark map</p>
</div>

## Overview

This project builds feature-based EKF SLAM on a TurtleBot3 from scratch. Five ROS 2 packages make up the system:

- **turtlelib** — Pure C++ library for SE(2) transforms, differential drive kinematics, and the EKF. No ROS dependency; fully unit-tested with Catch2.
- **nusim** — 2D physics simulator with Gaussian wheel noise, wheel slip, lidar ray-casting, and collision detection.
- **nuturtle_description** — Multi-colour TurtleBot3 URDF with a parametric `diff_params.yaml` for wheel radius, track width, and collision geometry.
- **nuturtle_control** — Turtle interface node, odometry node, and a circle-driving node.
- **nuslam** — Landmark detection pipeline and EKF SLAM node.

## Algorithms

### Odometry

The odometry node integrates wheel encoder deltas using the constant-curvature arc model from the `DiffDrive` class. It publishes `nav_msgs/Odometry` and broadcasts the `odom → base_footprint` TF, with an `initial_pose` service to reset the origin.

<div style="display: flex; gap: 16px; margin: 20px 0; flex-wrap: nowrap; align-items: flex-start;">
  <div style="flex: 0 0 30%; text-align: center;">
    <video class="img-responsive" autoplay loop muted playsinline style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12); width: 100%;">
      <source src="{{ site.url }}/img/portfolio/Irl_Turtle_spin.mp4" type="video/mp4">
    </video>
    <p style="margin-top: 8px; font-size: 0.9em; color: #666;">Physical TurtleBot3 driving in a circle</p>
  </div>
  <div style="flex: 0 0 68%; text-align: center;">
    <video class="img-responsive" autoplay loop muted playsinline style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12); width: 100%;">
      <source src="{{ site.url }}/img/portfolio/Rviz_Turtle_spin.mp4" type="video/mp4">
    </video>
    <p style="margin-top: 8px; font-size: 0.9em; color: #666;">Odometry estimate visualized in RViz</p>
  </div>
</div>

### Landmark Detection

Landmarks are cylinders detected from 2D lidar scans in three stages:

1. **Clustering** — consecutive scan points within a distance threshold form a cluster; clusters with fewer than 4 points are discarded.
2. **Circle fitting** — the Hyper algebraic fit finds the centre and radius of each cluster. Clusters with implausible radii are rejected.
3. **Arc classification** — uses the inscribed angle theorem: for a true circular arc, the angle ∠P₁PP₂ is nearly constant across all points P. Clusters whose mean falls between 90°–135° with standard deviation below 0.15 rad are classified as circles.

### EKF SLAM

The EKF maintains a joint state vector [θ, x, y, mx₁, my₁, …, mxN, myN] and a single covariance matrix over robot pose and all landmark positions simultaneously.

- **Prediction** — wheel encoder deltas propagate through the nonlinear motion model; the Jacobian is computed analytically.
- **Correction** — each detected landmark is matched to a known map entry by world-frame Euclidean distance, then used to correct the full state via a range-bearing Jacobian.
- **Initialisation** — on first sighting, a landmark is placed using the inverse measurement model and the EKF correction is skipped for that frame, avoiding a degenerate update with uninformative covariance.

## TF Tree

<div style="text-align: center; margin: 20px 0;">
  <a href="{{ site.url }}/img/portfolio/tf_tree.png" target="_blank" title="Click to view full size">
    <img src="{{ site.url }}/img/portfolio/tf_tree.png" style="width: 100%; border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.10); cursor: zoom-in;" alt="TF Tree">
  </a>
  <p style="margin-top: 8px; font-size: 0.85em; color: #999;">Click to view full size</p>
</div>

