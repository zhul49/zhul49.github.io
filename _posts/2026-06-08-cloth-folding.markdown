---
layout: post
modal-id: 6
date: 2026-06-08
title: Autonomous Cloth Folding
subtitle: A generalizable bimanual policy for the LeHome Challenge 2026
img: cloth_folding_thumbnail_v2.gif
hero: cloth_folding_hero.mp4
alt: Autonomous Cloth Folding
project-date: Jun 2026
description: "A bimanual robot policy that folds clothes from arbitrary crumpled states. Trained on simulation for the LeHome Challenge 2026 and handmade demos with benchmarking across Diffusion Policy, ACT, and SmolVLA."
tags:
  - Imitation Learning
  - SmolVLA
  - ACT
  - Diffusion Policy
  - Isaac Sim
  - LeRobot SO-101
---
## Overview

This is our entry for the **LeHome Challenge 2026**, a competition for robotic garment manipulation. The goal is a single policy that takes a piece of clothing from an arbitrary initial state, crumpled, twisted, or flat, and manipulates it into a correctly folded state using a pair of bimanual arms. Hardware is the LeRobot SO-ARM101, and submissions are scored by a mesh-keypoint pairwise-proximity metric against a target fold.

This was a team project: Conor Hayes, Andnet DeBoer, and myself, run as a Northwestern CS396 final project and robotics research project.

<div style="text-align: center; margin: 20px 0;">
  <img src="{{ site.url }}/img/portfolio/cloth_folding_thumbnail_v2.gif" class="img-responsive img-centered" alt="SmolVLA folding a garment in the LeHome Isaac Sim environment" style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">Our best policy, SmolVLA, folding a garment in the LeHome Isaac Sim environment</p>
</div>

## System Overview

Our pipeline has three stages:

1. **Data collection:** teleoperation in simulation using the SO-101 arms, plus procedural trajectory generation to scale up demonstrations.
2. **Pre-training + policy training:** we trained three policy families, SmolVLA, Diffusion Policy, and ACT, under domain randomization.
3. **Simulation evaluation:** SO-101 in **Isaac Sim**, scored against the competition's keypoint metric.

## Augmenting the Data with NVIDIA Cosmos

Collecting real teleoperation episodes by hand is slow, so we used NVIDIA Cosmos to grow our dataset. Cosmos takes one of our clips and re-renders it in a completely different setting while keeping the robot's motion exactly the same. From a single demo we can spin up dozens of variants with new backgrounds, lighting, colors, and textures. All that variety is what teaches the policy to handle scenes it never actually saw while training.

<div style="text-align: center; margin: 20px 0;">
  <img src="{{ site.url }}/img/portfolio/Nvidia-Cosmos.gif" class="img-responsive img-centered" alt="NVIDIA Cosmos data augmentation example" style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">An example of our NVIDIA Cosmos augmentation. The same manipulation, re-rendered with a different background and lighting.</p>
</div>

## Comparing the Policies

We trained and tested three imitation-learning policies: SmolVLA, ACT, and Diffusion Policy. SmolVLA, shown in the overview above, and ACT both folded the garment cleanly and did it the same way every time. Diffusion Policy struggled. It usually bunched or dragged the cloth instead of folding it, and once the fabric ended up in an odd shape it almost never recovered.

<div style="text-align: center; margin: 20px 0;">
  <img src="{{ site.url }}/img/portfolio/act_edit.gif" class="img-responsive img-centered" alt="ACT policy folding a garment" style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">ACT folds cleanly and decisively.</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="{{ site.url }}/img/portfolio/DP_edit.gif" class="img-responsive img-centered" alt="Diffusion Policy struggling to fold a garment" style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">Diffusion Policy often leaves the garment bunched instead of folded.</p>
</div>

So why the gap? ACT plans a short burst of motion at a time, which fits the smooth, repetitive rhythm of folding really well. SmolVLA leans on a big pre-trained vision-language model, so it handles new starting positions with ease. Diffusion Policy builds each move through many small refinement steps, and that process gets fragile when the cloth is partly hidden or hard to read. A small mistake early on snowballs into the messy folds you see here.

## Results

Submissions are scored with a mesh-keypoint metric. We place a set of check points on the garment, and a fold passes a check when each point lands close enough to where it should be. The more points that match their targets, the higher the score.

<div style="text-align: center; margin: 20px 0;">
  <img src="{{ site.url }}/img/portfolio/Points_on_clothes.png" class="img-responsive img-centered" alt="Mesh keypoint check points used to score a fold" style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12); max-width: 640px;">
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">How the scoring works. Each check point on the garment has to land close to its target position.</p>
</div>

Across our evaluation episodes, the three policies landed right where the folds above suggested:

<div style="overflow-x: auto; margin: 24px 0;">
<table style="border-collapse: collapse; margin: 0 auto; font-size: 1em; min-width: 440px;">
  <thead>
    <tr style="background: #2c3e50; color: #fff;">
      <th style="text-align: left; padding: 12px 28px;">Policy</th>
      <th style="text-align: center; padding: 12px 28px;">Success rate</th>
      <th style="text-align: center; padding: 12px 28px;">Fold quality</th>
    </tr>
  </thead>
  <tbody>
    <tr style="background: #eafaf5; border-bottom: 1px solid #e3e8ec;">
      <td style="text-align: left; padding: 12px 28px; font-weight: 700;">SmolVLA</td>
      <td style="text-align: center; padding: 12px 28px;">69.44%</td>
      <td style="text-align: center; padding: 12px 28px;">8 / 10</td>
    </tr>
    <tr style="border-bottom: 1px solid #e3e8ec;">
      <td style="text-align: left; padding: 12px 28px; font-weight: 700;">ACT</td>
      <td style="text-align: center; padding: 12px 28px;">61.11%</td>
      <td style="text-align: center; padding: 12px 28px;">7 / 10</td>
    </tr>
    <tr>
      <td style="text-align: left; padding: 12px 28px; font-weight: 700;">Diffusion</td>
      <td style="text-align: center; padding: 12px 28px;">41.67%</td>
      <td style="text-align: center; padding: 12px 28px;">2 / 10</td>
    </tr>
  </tbody>
</table>
</div>

SmolVLA came out on top, ACT was close behind, and Diffusion Policy trailed well back. That lines up with what the clips show.
