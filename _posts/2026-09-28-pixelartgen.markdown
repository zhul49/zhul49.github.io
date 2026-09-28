---
layout: post
modal-id: 7
date: 2026-09-28
title: PixelArtGen
subtitle: An image-to-image diffusion model that turns Pokémon artwork into pixel-art sprites
img: pixelartgen_thumb.png
hero: pixelartgen_teaser.png
alt: PixelArtGen artwork-to-sprite diffusion model
project-date: Sep 2026
description: "A conditional image-to-image diffusion model that turns official Pokémon front-view artwork into 96×96 pixel-art sprites. It uses a UNet with cross-attention onto an encoded copy of the artwork, trained on regular and shiny artwork/sprite pairs, so it can sprite Pokémon it has never seen."
github: https://github.com/zhul49/PixelArtGen
tags:
  - Conditional Diffusion
  - Image-to-Image
  - Cross-Attention
  - UNet
  - DDIM Sampling
  - PyTorch
---
## Overview

PixelArtGen turns the front-view of official Pokémon artwork into 96×96 3DS-style pixel-art sprites. It is a conditional image-to-image diffusion model: instead of denoising from text, it denoises a 96×96 sprite while continuously looking at an encoded copy of the source artwork. Because the artwork is the condition rather than the starting image, the model can produce a proper low-resolution sprite with hard pixel edges rather than just downscaling the original.

I trained it on paired official artwork and game sprites, using both regular and shiny forms, so it learns the mapping from a clean illustration to the blocky in-game look and can generate sprites for Pokémon that have no official sprite yet.

## Gen 10 Starters

The real test is generalization to Pokémon that were never in the training set. I fed the model the freshly released official artwork for the three Gen 10 starters. Nothing about these Pokémon was seen during training, so every sprite below is produced purely from the artwork on the left.

<div style="margin: 24px 0;">
  <div style="display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 18px;">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_browt.png" alt="Browt official artwork" style="width: 200px; height: 200px; object-fit: contain; border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <span style="font-size: 2em; color: #18bc9c; font-weight: 700;">&rarr;</span>
    <img src="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" alt="Browt generated sprite 1" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite2.webp" alt="Browt generated sprite 2" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite3.webp" alt="Browt generated sprite 3" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  </div>
  <p style="text-align: center; margin-top: 8px; font-size: 0.9em; color: #666;">Browt (grass), with the official artwork on the left and three sprites generated from it.</p>
</div>

<div style="margin: 24px 0;">
  <div style="display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 18px;">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_pombon.png" alt="Pombon official artwork" style="width: 200px; height: 200px; object-fit: contain; border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <span style="font-size: 2em; color: #18bc9c; font-weight: 700;">&rarr;</span>
    <img src="{{ site.url }}/img/portfolio/pixelartgen_pombon_sprite1.webp" alt="Pombon generated sprite 1" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_pombon_sprite2.webp" alt="Pombon generated sprite 2" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_pombon_sprite3.webp" alt="Pombon generated sprite 3" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  </div>
  <p style="text-align: center; margin-top: 8px; font-size: 0.9em; color: #666;">Pombon (fire), with the official artwork on the left and three sprites generated from it.</p>
</div>

<div style="margin: 24px 0;">
  <div style="display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 18px;">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_gecqua.png" alt="Gecqua official artwork" style="width: 200px; height: 200px; object-fit: contain; border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <span style="font-size: 2em; color: #18bc9c; font-weight: 700;">&rarr;</span>
    <img src="{{ site.url }}/img/portfolio/pixelartgen_gecqua_sprite1.webp" alt="Gecqua generated sprite 1" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_gecqua_sprite2.webp" alt="Gecqua generated sprite 2" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
    <img src="{{ site.url }}/img/portfolio/pixelartgen_gecqua_sprite3.webp" alt="Gecqua generated sprite 3" style="width: 120px; height: 120px; image-rendering: pixelated; border-radius: 6px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  </div>
  <p style="text-align: center; margin-top: 8px; font-size: 0.9em; color: #666;">Gecqua (water), with the official artwork on the left and three sprites generated from it.</p>
</div>

## Architecture

The core is a conditional UNet that works at the 96×96 sprite resolution and predicts the noise added to a sprite at a given timestep. It has three resolution levels with channel widths of 64, 128, and 256, two residual blocks per level, and a bottleneck at the smallest spatial size.

A few choices inside the residual blocks are deliberate. I use GroupNorm instead of BatchNorm because in diffusion every image in a batch carries a different amount of noise, so batch statistics are misleading, whereas group statistics stay stable per sample. Activations are SiLU rather than ReLU because it is smooth everywhere, which suits the regression-style noise prediction, and each block carries a small dropout to fight overfitting on a fairly small dataset. The timestep is turned into a sinusoidal embedding, passed through a small MLP, and injected into every residual block as a per-channel bias so the network always knows how noisy the current sprite is.

**Conditioning on the artwork.** A separate CNN encoder compresses the 256×256 artwork down to a 16×16 feature map with 256 channels. That encoded artwork is then fed into the UNet through cross-attention, which is the piece that made the project actually work. In each cross-attention block the queries come from the sprite being denoised, while the keys and values come from the artwork features. In other words, every location in the sprite gets to ask the artwork "what belongs here," and pull back the matching shape and color. I place cross-attention at the deepest downsampling level, the bottleneck, and the first upsampling level, where the spatial size is small enough that attention is cheap. Multi-head self-attention runs alongside it at the same levels.

**Keeping edges crisp.** On the decoder side I upsample with nearest-neighbor followed by a convolution instead of bilinear upsampling or a transposed conv. Bilinear smooths everything, which is exactly wrong for pixel art, whereas nearest-neighbor preserves the hard blocky edges and lets the following conv clean up the result.

<div style="max-width: 900px; margin: 28px auto;">
<svg viewBox="0 0 900 500" role="img" aria-label="Conditional UNet architecture with cross-attention onto encoded artwork" style="width:100%; height:auto; font-family: Lato, Helvetica, Arial, sans-serif;">
  <defs>
    <marker id="ar1" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#2c3e50"/></marker>
    <marker id="arT1" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#18bc9c"/></marker>
    <marker id="arG1" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#9aa7b0"/></marker>
  </defs>

  <!-- condition lane -->
  <rect x="250" y="20" width="130" height="44" rx="8" fill="#eafaf5" stroke="#18bc9c" stroke-width="2"/>
  <text x="315" y="40" text-anchor="middle" font-size="12.5" fill="#2c3e50" font-weight="700">Official artwork</text>
  <text x="315" y="56" text-anchor="middle" font-size="11" fill="#555">256 × 256</text>
  <line x1="380" y1="42" x2="398" y2="42" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <rect x="400" y="20" width="150" height="44" rx="8" fill="#eafaf5" stroke="#18bc9c" stroke-width="2"/>
  <text x="475" y="40" text-anchor="middle" font-size="12.5" fill="#2c3e50" font-weight="700">Artwork encoder</text>
  <text x="475" y="56" text-anchor="middle" font-size="11" fill="#555">5 stride-2 convs</text>
  <line x1="550" y1="42" x2="573" y2="42" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <rect x="575" y="20" width="155" height="44" rx="8" fill="#2c3e50"/>
  <text x="652" y="39" text-anchor="middle" font-size="12.5" fill="#fff" font-weight="700">Artwork features</text>
  <text x="652" y="55" text-anchor="middle" font-size="11" fill="#cfe9e2">16 × 16 × 256</text>

  <!-- io row -->
  <rect x="110" y="105" width="190" height="44" rx="8" fill="#fff" stroke="#2c3e50" stroke-width="2"/>
  <text x="205" y="125" text-anchor="middle" font-size="12.5" fill="#2c3e50" font-weight="700">Noisy sprite 96 × 96</text>
  <text x="205" y="141" text-anchor="middle" font-size="11" fill="#555">+ timestep t</text>
  <rect x="600" y="105" width="190" height="44" rx="8" fill="#fff" stroke="#18bc9c" stroke-width="2"/>
  <text x="695" y="131" text-anchor="middle" font-size="12.5" fill="#2c3e50" font-weight="700">Predicted noise 96 × 96</text>

  <!-- unet container -->
  <rect x="70" y="172" width="760" height="300" rx="12" fill="#f7fbfa" stroke="#cfd8dc" stroke-width="1.5"/>
  <text x="450" y="463" text-anchor="middle" font-size="11.5" fill="#7a8891" font-style="italic">Conditional UNet: predicts the noise added to the sprite</text>

  <!-- encoder col -->
  <rect x="120" y="200" width="170" height="40" rx="7" fill="#eafaf5" stroke="#18bc9c" stroke-width="1.6"/>
  <text x="205" y="225" text-anchor="middle" font-size="12" fill="#2c3e50">Down · 64 · 96²</text>
  <rect x="120" y="262" width="170" height="40" rx="7" fill="#eafaf5" stroke="#18bc9c" stroke-width="1.6"/>
  <text x="205" y="287" text-anchor="middle" font-size="12" fill="#2c3e50">Down · 128 · 48²</text>
  <rect x="120" y="324" width="170" height="40" rx="7" fill="#d5f3ea" stroke="#18bc9c" stroke-width="2"/>
  <text x="205" y="349" text-anchor="middle" font-size="12" fill="#2c3e50">Down · 256 · 24² <tspan font-weight="700" fill="#12876f">+attn</tspan></text>

  <!-- bottleneck -->
  <rect x="365" y="398" width="210" height="46" rx="8" fill="#2c3e50"/>
  <text x="470" y="418" text-anchor="middle" font-size="12" fill="#fff" font-weight="700">Bottleneck · 256</text>
  <text x="470" y="434" text-anchor="middle" font-size="11" fill="#cfe9e2">self-attn + cross-attn</text>

  <!-- decoder col -->
  <rect x="610" y="324" width="170" height="40" rx="7" fill="#d5f3ea" stroke="#18bc9c" stroke-width="2"/>
  <text x="695" y="349" text-anchor="middle" font-size="12" fill="#2c3e50">Up · 256 <tspan font-weight="700" fill="#12876f">+attn</tspan></text>
  <rect x="610" y="262" width="170" height="40" rx="7" fill="#eafaf5" stroke="#18bc9c" stroke-width="1.6"/>
  <text x="695" y="287" text-anchor="middle" font-size="12" fill="#2c3e50">Up · 128 · 48²</text>
  <rect x="610" y="200" width="170" height="40" rx="7" fill="#eafaf5" stroke="#18bc9c" stroke-width="1.6"/>
  <text x="695" y="225" text-anchor="middle" font-size="12" fill="#2c3e50">Up · 64 · 96²</text>

  <!-- data flow -->
  <line x1="205" y1="149" x2="205" y2="200" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="205" y1="240" x2="205" y2="262" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="205" y1="302" x2="205" y2="324" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="240" y1="364" x2="415" y2="400" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="525" y1="400" x2="690" y2="366" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="695" y1="324" x2="695" y2="302" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="695" y1="262" x2="695" y2="240" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <line x1="695" y1="200" x2="695" y2="149" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>

  <!-- skip connections -->
  <line x1="290" y1="220" x2="608" y2="220" stroke="#9aa7b0" stroke-width="1.6" stroke-dasharray="5 4" marker-end="url(#arG1)"/>
  <line x1="290" y1="282" x2="608" y2="282" stroke="#9aa7b0" stroke-width="1.6" stroke-dasharray="5 4" marker-end="url(#arG1)"/>
  <line x1="290" y1="344" x2="608" y2="344" stroke="#9aa7b0" stroke-width="1.6" stroke-dasharray="5 4" marker-end="url(#arG1)"/>
  <text x="450" y="214" text-anchor="middle" font-size="10.5" fill="#7a8891">skip connections</text>

  <!-- cross attention -->
  <line x1="652" y1="64" x2="490" y2="396" stroke="#18bc9c" stroke-width="2" stroke-dasharray="6 4" marker-end="url(#arT1)"/>
  <text x="600" y="250" text-anchor="middle" font-size="11" fill="#12876f" font-weight="700" transform="rotate(64 600 250)">cross-attention</text>

  <!-- legend -->
  <line x1="90" y1="484" x2="120" y2="484" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar1)"/>
  <text x="126" y="488" font-size="10.5" fill="#555">data flow</text>
  <line x1="210" y1="484" x2="240" y2="484" stroke="#18bc9c" stroke-width="2" stroke-dasharray="6 4" marker-end="url(#arT1)"/>
  <text x="246" y="488" font-size="10.5" fill="#555">artwork condition (also feeds the +attn blocks)</text>
  <line x1="560" y1="484" x2="590" y2="484" stroke="#9aa7b0" stroke-width="1.6" stroke-dasharray="5 4" marker-end="url(#arG1)"/>
  <text x="596" y="488" font-size="10.5" fill="#555">skip · t injected into every block</text>
</svg>
<p style="text-align: center; margin-top: 6px; font-size: 0.9em; color: #666;">The artwork is encoded once, then read by the sprite through cross-attention at the deepest blocks and the bottleneck.</p>
</div>

## Training

Data is built by pairing each official artwork with its game sprite by Pokédex ID, and I include shiny forms as additional pairs, which roughly doubles the data and forces the model to key off shape rather than memorizing a single color per Pokémon. Artwork is resized to 256×256 with bicubic interpolation so it stays clean, while the target sprite is resized to 96×96 with nearest-neighbor so its pixels stay intact. Transparent backgrounds are composited onto solid black, and everything is normalized to the range -1 to 1. Data is split 90/10 into train and validation by Pokémon, so validation Pokémon are never seen during training.

Augmentation is paired carefully. Horizontal flips are applied to the artwork and its sprite together so they stay aligned, but color jitter (brightness, contrast, and saturation) is applied only to the input artwork and never the target. That teaches the model to be robust to lighting and color shifts in the input without ever corrupting the sprite it is supposed to reproduce.

The diffusion process uses a continuous-time cosine schedule, where the signal and noise rates are the cosine and sine of the timestep. Timesteps are sampled uniformly in the range 0 to 1, noise is added to the sprite, and the model is trained to predict that noise with an L1 loss, which is more forgiving of the occasional hard outlier pixel than an L2 loss. Optimization is AdamW at a 2e-4 learning rate with weight decay, a linear warmup over the first 1000 steps followed by a cosine decay down to a tenth of the base rate, and gradient clipping for stability. I keep an exponential moving average of the weights with a decay of 0.999, and it is that EMA copy, not the raw training weights, that gets used for all sampling.

<div style="max-width: 900px; margin: 28px auto;">
<svg viewBox="0 0 900 320" role="img" aria-label="Training loop: noise the sprite, predict the noise, take an L1 loss, update, keep an EMA copy" style="width:100%; height:auto; font-family: Lato, Helvetica, Arial, sans-serif;">
  <defs>
    <marker id="ar2" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#2c3e50"/></marker>
    <marker id="arT2" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#e08a2b"/></marker>
  </defs>

  <!-- data source -->
  <rect x="15" y="95" width="150" height="120" rx="8" fill="#eafaf5" stroke="#18bc9c" stroke-width="2"/>
  <text x="90" y="120" text-anchor="middle" font-size="12" fill="#2c3e50" font-weight="700">Artwork + sprite</text>
  <text x="90" y="137" text-anchor="middle" font-size="12" fill="#2c3e50" font-weight="700">pairs</text>
  <text x="90" y="158" text-anchor="middle" font-size="10.5" fill="#555">regular + shiny</text>
  <text x="90" y="174" text-anchor="middle" font-size="10.5" fill="#555">90 / 10 split</text>
  <text x="90" y="190" text-anchor="middle" font-size="10.5" fill="#555">paired flip +</text>
  <text x="90" y="204" text-anchor="middle" font-size="10.5" fill="#555">input-only jitter</text>

  <!-- noise step -->
  <rect x="200" y="100" width="175" height="90" rx="8" fill="#fff" stroke="#2c3e50" stroke-width="2"/>
  <text x="287" y="126" text-anchor="middle" font-size="12" fill="#2c3e50" font-weight="700">Noise the sprite</text>
  <text x="287" y="146" text-anchor="middle" font-size="11" fill="#555">xₜ = signal·x₀ + noise·ε</text>
  <text x="287" y="164" text-anchor="middle" font-size="11" fill="#555">cosine schedule</text>
  <text x="287" y="180" text-anchor="middle" font-size="11" fill="#555">t ∼ Uniform[0, 1]</text>

  <!-- unet -->
  <rect x="410" y="100" width="160" height="90" rx="8" fill="#2c3e50"/>
  <text x="490" y="130" text-anchor="middle" font-size="12.5" fill="#fff" font-weight="700">UNet</text>
  <text x="490" y="150" text-anchor="middle" font-size="10.5" fill="#cfe9e2">(xₜ, t, artwork)</text>
  <text x="490" y="168" text-anchor="middle" font-size="10.5" fill="#cfe9e2">→ predicted noise ε̂</text>

  <!-- loss -->
  <rect x="605" y="110" width="120" height="70" rx="8" fill="#fdeede" stroke="#e08a2b" stroke-width="2"/>
  <text x="665" y="140" text-anchor="middle" font-size="12.5" fill="#8a5212" font-weight="700">L1 loss</text>
  <text x="665" y="159" text-anchor="middle" font-size="11" fill="#8a5212">ε̂ vs ε</text>

  <!-- optimizer -->
  <rect x="760" y="100" width="128" height="90" rx="8" fill="#eafaf5" stroke="#18bc9c" stroke-width="2"/>
  <text x="824" y="126" text-anchor="middle" font-size="11.5" fill="#2c3e50" font-weight="700">AdamW</text>
  <text x="824" y="145" text-anchor="middle" font-size="10.5" fill="#555">warmup +</text>
  <text x="824" y="159" text-anchor="middle" font-size="10.5" fill="#555">cosine LR</text>
  <text x="824" y="175" text-anchor="middle" font-size="10.5" fill="#555">grad clip</text>

  <!-- EMA -->
  <rect x="605" y="235" width="180" height="60" rx="8" fill="#d5f3ea" stroke="#18bc9c" stroke-width="2"/>
  <text x="695" y="260" text-anchor="middle" font-size="11.5" fill="#2c3e50" font-weight="700">EMA weights (0.999)</text>
  <text x="695" y="278" text-anchor="middle" font-size="10.5" fill="#555">used for all sampling</text>

  <!-- flows -->
  <line x1="165" y1="145" x2="198" y2="145" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar2)"/>
  <text x="182" y="137" text-anchor="middle" font-size="9.5" fill="#7a8891">x₀</text>
  <!-- artwork condition over the top -->
  <path d="M120,95 L120,60 L490,60 L490,100" fill="none" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar2)"/>
  <text x="300" y="52" text-anchor="middle" font-size="10.5" fill="#555">artwork (condition)</text>
  <line x1="375" y1="145" x2="408" y2="145" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar2)"/>
  <text x="391" y="137" text-anchor="middle" font-size="9.5" fill="#7a8891">xₜ</text>
  <line x1="570" y1="145" x2="603" y2="145" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar2)"/>
  <text x="587" y="137" text-anchor="middle" font-size="9.5" fill="#7a8891">ε̂</text>
  <!-- true noise into loss from below -->
  <path d="M287,190 L287,215 L665,215 L665,182" fill="none" stroke="#e08a2b" stroke-width="1.8" stroke-dasharray="6 4" marker-end="url(#arT2)"/>
  <text x="470" y="230" text-anchor="middle" font-size="10.5" fill="#8a5212">true noise ε (the target)</text>
  <line x1="725" y1="145" x2="758" y2="145" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar2)"/>
  <!-- update weights feedback -->
  <path d="M824,190 L824,268 L787,268" fill="none" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar2)"/>
  <path d="M824,190 L824,300 L490,300 L490,192" fill="none" stroke="#2c3e50" stroke-width="1.8" stroke-dasharray="6 4" marker-end="url(#ar2)"/>
  <text x="560" y="313" text-anchor="middle" font-size="10.5" fill="#7a8891">update weights (backprop)</text>
</svg>
<p style="text-align: center; margin-top: 6px; font-size: 0.9em; color: #666;">Each step noises a sprite to a random level, asks the UNet to predict that noise from the noisy sprite plus the artwork, and trains on the L1 gap. A slow EMA copy of the weights is what actually gets used to generate.</p>
</div>

## Generating sprites

At inference the model starts from pure Gaussian noise at 96×96 and runs a deterministic DDIM sampler. At each step it predicts the noise, reconstructs an estimate of the clean sprite, clamps it to the valid range, and takes a deterministic step toward the next, lower noise level. The whole trajectory is conditioned on the same encoded artwork the entire way down. Sampling defaults to 50 steps but works anywhere from 10 to 100, trading speed for quality.

To produce variety, I generate several samples at once from the same artwork by starting each one from a different random noise seed. The artwork condition is shared, so every sample is a valid sprite of the same Pokémon, but small differences in shading and posture appear across them.

<div style="max-width: 900px; margin: 28px auto;">
<svg viewBox="0 0 900 430" role="img" aria-label="Sampling: an artwork conditions a DDIM denoising loop that turns noise into a sprite" style="width:100%; height:auto; font-family: Lato, Helvetica, Arial, sans-serif;">
  <defs>
    <marker id="ar3" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#2c3e50"/></marker>
    <marker id="arT3" markerWidth="10" markerHeight="10" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 Z" fill="#18bc9c"/></marker>
    <filter id="grain" x="0" y="0" width="100%" height="100%">
      <feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2" stitchTiles="stitch" result="n"/>
      <feColorMatrix in="n" type="saturate" values="0.15"/>
    </filter>
    <clipPath id="tile"><rect x="0" y="0" width="120" height="120" rx="8"/></clipPath>
  </defs>

  <!-- worked example row -->
  <image href="{{ site.url }}/img/portfolio/pixelartgen_browt.png" x="30" y="30" width="120" height="120" preserveAspectRatio="xMidYMid slice" clip-path="url(#tile)"/>
  <rect x="30" y="30" width="120" height="120" rx="8" fill="none" stroke="#18bc9c" stroke-width="2"/>
  <text x="90" y="168" text-anchor="middle" font-size="11" fill="#555">artwork (condition)</text>

  <line x1="152" y1="90" x2="205" y2="90" stroke="#18bc9c" stroke-width="2.5" stroke-dasharray="6 4" marker-end="url(#arT3)"/>

  <rect x="210" y="30" width="330" height="120" rx="10" fill="#f7fbfa" stroke="#18bc9c" stroke-width="2"/>
  <text x="375" y="55" text-anchor="middle" font-size="13" fill="#2c3e50" font-weight="700">DDIM sampler (deterministic)</text>
  <text x="228" y="80" font-size="11.5" fill="#444">1 · start from Gaussian noise (96²)</text>
  <text x="228" y="100" font-size="11.5" fill="#444">2 · repeat ~50 steps:</text>
  <text x="240" y="118" font-size="11.5" fill="#444">predict noise → estimate x₀ → step to lower t</text>
  <text x="228" y="140" font-size="11" fill="#12876f" font-style="italic">the artwork conditions every step</text>

  <line x1="540" y1="90" x2="588" y2="90" stroke="#2c3e50" stroke-width="2.5" marker-end="url(#ar3)"/>

  <image href="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" x="600" y="30" width="120" height="120" preserveAspectRatio="xMidYMid slice" clip-path="url(#tile)" style="image-rendering: pixelated;"/>
  <rect x="600" y="30" width="120" height="120" rx="8" fill="none" stroke="#2c3e50" stroke-width="2"/>
  <text x="660" y="168" text-anchor="middle" font-size="11" fill="#555">generated sprite (96²)</text>

  <!-- trajectory -->
  <text x="450" y="222" text-anchor="middle" font-size="12" fill="#2c3e50" font-weight="700">Denoising trajectory (illustrative)</text>

  <g>
    <!-- tile positions: 60,220,380,540,700 ; y=245 -->
    <image href="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" x="60" y="245" width="110" height="110" preserveAspectRatio="xMidYMid slice" style="image-rendering: pixelated;"/>
    <rect x="60" y="245" width="110" height="110" rx="7" filter="url(#grain)" opacity="1"/>
    <rect x="60" y="245" width="110" height="110" rx="7" fill="none" stroke="#cfd8dc" stroke-width="1.5"/>
    <text x="115" y="372" text-anchor="middle" font-size="10.5" fill="#666">t = 0.99</text>

    <image href="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" x="220" y="245" width="110" height="110" preserveAspectRatio="xMidYMid slice" style="image-rendering: pixelated;"/>
    <rect x="220" y="245" width="110" height="110" rx="7" filter="url(#grain)" opacity="0.68"/>
    <rect x="220" y="245" width="110" height="110" rx="7" fill="none" stroke="#cfd8dc" stroke-width="1.5"/>
    <text x="275" y="372" text-anchor="middle" font-size="10.5" fill="#666">t ≈ 0.75</text>

    <image href="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" x="380" y="245" width="110" height="110" preserveAspectRatio="xMidYMid slice" style="image-rendering: pixelated;"/>
    <rect x="380" y="245" width="110" height="110" rx="7" filter="url(#grain)" opacity="0.42"/>
    <rect x="380" y="245" width="110" height="110" rx="7" fill="none" stroke="#cfd8dc" stroke-width="1.5"/>
    <text x="435" y="372" text-anchor="middle" font-size="10.5" fill="#666">t ≈ 0.50</text>

    <image href="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" x="540" y="245" width="110" height="110" preserveAspectRatio="xMidYMid slice" style="image-rendering: pixelated;"/>
    <rect x="540" y="245" width="110" height="110" rx="7" filter="url(#grain)" opacity="0.2"/>
    <rect x="540" y="245" width="110" height="110" rx="7" fill="none" stroke="#cfd8dc" stroke-width="1.5"/>
    <text x="595" y="372" text-anchor="middle" font-size="10.5" fill="#666">t ≈ 0.25</text>

    <image href="{{ site.url }}/img/portfolio/pixelartgen_browt_sprite1.webp" x="700" y="245" width="110" height="110" preserveAspectRatio="xMidYMid slice" style="image-rendering: pixelated;"/>
    <rect x="700" y="245" width="110" height="110" rx="7" fill="none" stroke="#18bc9c" stroke-width="2"/>
    <text x="755" y="372" text-anchor="middle" font-size="10.5" fill="#666">t = 0.00</text>

    <line x1="172" y1="300" x2="216" y2="300" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar3)"/>
    <line x1="332" y1="300" x2="376" y2="300" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar3)"/>
    <line x1="492" y1="300" x2="536" y2="300" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar3)"/>
    <line x1="652" y1="300" x2="696" y2="300" stroke="#2c3e50" stroke-width="2" marker-end="url(#ar3)"/>
  </g>

  <text x="450" y="398" text-anchor="middle" font-size="10.5" fill="#7a8891" font-style="italic">Noise is progressively removed while the artwork holds the shape and colors in place (frames shown are a schematic, not model captures).</text>
</svg>
<p style="text-align: center; margin-top: 6px; font-size: 0.9em; color: #666;">A worked example: Browt's artwork conditions a chain of denoising steps that turns pure noise into its sprite.</p>
</div>

## PixelForge, the GUI

I wrapped the model in a Gradio interface called PixelForge so it is usable without touching the code. You upload official front-view artwork, set the number of diffusion steps and how many samples you want, and it returns a strip of generated sprites. It works best with artwork at 256×256 or larger, since smaller inputs get upscaled and lose detail. The interface also reproduces the training preprocessing at upload time: it keys out the near-white background to transparency, composites onto black, and resizes to 256×256, so what the model sees at inference matches what it saw during training. Outputs are shown upscaled with nearest-neighbor so the pixel grid stays sharp on screen.

<div style="text-align: center; margin: 20px 0;">
  <img src="{{ site.url }}/img/portfolio/pixelartgen_gui.png" class="img-responsive img-centered" alt="The PixelForge Gradio interface" style="border-radius: 8px; box-shadow: 0 4px 14px rgba(0,0,0,0.12);">
  <p style="margin-top: 8px; font-size: 0.9em; color: #666;">PixelForge: upload artwork, tune the diffusion settings, and generate a strip of sprites.</p>
</div>

## What made it work

Two problems dominated the project. The first was spatial awareness. Early versions produced sprites with roughly the right colors but no sense of where the ears, legs, arms, and head actually belonged, because the model was leaning on a single compressed summary of the artwork. Adding cross-attention, so the sprite could reference the full artwork feature map throughout denoising, fixed most of the misplaced-anatomy problems. The second was sharpness: the first outputs were soft and blurry, the opposite of pixel art. Switching the decoder to nearest-neighbor upsampling followed by a convolution, and resizing the sprite targets with nearest-neighbor rather than a smoothing filter, brought back the crisp blocky edges that make it read as a real sprite.
