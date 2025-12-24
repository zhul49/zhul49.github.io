---
layout: post
modal-id: 2
date: 2025-12-18
title: Jack-in-the-Box Physics Simulation
img: jackbox.gif
alt: Jack-in-the-Box Simulation
project-date: Dec 2025
#client: "Physics-Based Robotics Simulation"
#category: "Dynamics • Simulation • Control"

description: "A physics-based simulation of a jack-in-the-box that realistically models bouncing and collisions using real-world motion principles."

#tech: "Rigid body dynamics · Impact modeling · Euler–Lagrange equations · SE(3) transformations · Numerical simulation · Python"

tags:
  - Euler–Lagrange
  - Rigid-Body Dynamics
  - Impulse Impacts
  - Coordinate Frames

github: https://github.com/zhul49/Jack-in-the-Box
---
## Project Summary
This project simulates a jack-in-the-box mechanism to study the interaction between rigid-body motion and internal impacts. The system’s motion is computed from analytical dynamics, with collisions between the jack and the box resolved using impulse-based methods.

The result is a compact simulation that highlights the role of coordinate frames, equations of motion, and contact dynamics in mechanical behavior.

## Frames, Dynamics, and Impacts
The system is represented using multiple coordinate frames. A fixed world frame defines the inertial reference. A box frame moves and rotates with the enclosure. A jack frame rotates inside the box and defines the positions of the four tip masses. Points are mapped between frames using rigid-body transformations of the form

<p style="text-align:center;">
  p<sub>world</sub> = R · p<sub>body</sub> + t
</p>

Expressing the jack in the box frame simplifies contact detection, since the box walls are fixed in that frame.

The motion of the box and jack is derived using the Euler–Lagrange formulation,

<p style="text-align:center;">
  d/dt(∂L/∂q̇) − ∂L/∂q = Q
</p>

which governs smooth translational and rotational motion between collisions. These equations are numerically integrated forward in time.

When a jack tip contacts a wall, the collision is treated as an instantaneous event. Instead of integrating through contact, velocities are updated using an impulse-based formulation. The post-impact generalized velocities satisfy

<p style="text-align:center;">
  ∂L/∂q̇⁺ = ∂L/∂q̇⁻ + Jᵀλ
</p>

where \(J\) is the contact Jacobian and \(λ\) is the impulse magnitude. The impulse is solved by enforcing the contact constraint together with an energy consistency condition, resulting in realistic momentum transfer between the internal jack and the box. These repeated impacts produce rotation, bouncing, and jitter of the enclosure.

![Jack Frames](/img/portfolio/jackframes.png)

