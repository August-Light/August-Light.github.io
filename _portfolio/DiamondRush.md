---
title: "Diamond Rush"
excerpt: "A grid-based game built using Python<br/><img src='/images/portfolio/diamond_rush_cover.png'>"
collection: portfolio
date: 2025-06-06
---

# Overview

Diamond Rush is a grid-based game built using Python. This project is built in 2021 as a learning experience and personal challenge. It's a milestone in my journey of programming.

- Platform: Desktop
- Technology: Python (with Pygame library)
- Target: Survive in periodic danger zones and collect $50$ diamonds

<img src="/images/portfolio/diamond_rush.gif" width="270"/>

# Game Mechanics

- Player & Objective
  - A diamond appears at a random location on the grid.
  - The player controls Steve, starting at the center of the $5 \times 5$ grid.
  - The player needs to move Steve to the diamond to collect it.
  - After that, a new diamonds spawns at a new random location.
  - When $50$ diamonds are collected, the player wins.
- Danger Zone
  - Every few seconds, a danger zone appear randomly on the grid (marked in red). The danger zone occupies entire rows or columns.
  - Steve has $1$ second to exit the danger zone, or they will be "killed".

# Game Modes

- Baby Mode: The danger zone appears every $2.5$ seconds.
- Normal Mode: The danger zone appears every $1.5$ seconds.
- Master Mode: The danger zone appears every $1$ second, which means there is always a danger zone on the grid.
- Impossible Mode: Same spawn rate as Master Mode, but Steve is invisible most of the time, only becoming visible for $0.5$ second every $1.5$ seconds.

# What I learned?

- Implemented loops and dealt with player inputs.
- Used variables to correctly label the state of the player and the danger zone.

Furthermore, this is my very first time to build a complete project from scratch.

# Reflection

The structure of code is too messy: too many global variables, poor readability, and magic numbers appearing everywhere.  
Looking back, I would now restructure the code with classes, encapsulate state management, and separate the behind logic from display functions.

# Source Code

[Source Code](https://github.com/August-Light/DiamondRush)