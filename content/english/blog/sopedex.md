---
title: "Learning to Singulate Objects in Packed Environments using a Dexterous Hand"
meta_title: "SOPE-Dex"
description: "We present a novel approach to singulate objects in cluttered environments using a dexterous hand."
date: 2024-10-01T05:00:00Z
image: "/images/sopedex/sopedex-method.png"
categories: ["Research"]
author: "Hanyang ZHOU"
tags: ["Dexterous Hand", "Robotics"]
draft: false
---

This paper presents the **Singulating Objects in Packed Environments (SOPE) framework**, which utilizes a novel displacement-based state representation and a multi-phase RL approach to enable effective singulation of target objects in cluttered environments using a 16-DOF Allegro Hand.

The proposed method demonstrates high success rates in both simulation and real-world experiments, outperforming alternative techniques.

{{< accordion "Where can you find MORE interseting videos?" >}}

**See more excellent videos on our** [Project Website](https://sope-dex.github.io/)

{{< /accordion >}}

## About this Project

Robotic object singulation, where a robot must isolate, grasp, and retrieve a target object in a cluttered environment, is a fundamental challenge in robotic manipulation.

This task is difficult due to occlusions and how other objects act as obstacles for manipulation. A robot must also reason about the effect of object-object interactions as it tries to singulate the target.

Prior work has explored object singulation in scenarios where there is enough free space to perform relatively long pushes to separate objects, in contrast to when space is tight and objects have little separation from each other.

In this paper, we propose the Singulating Objects in Packed Environments (SOPE) framework. We propose a novel method that involves a displacement-based state representation and a multi-phase reinforcement learning procedure that enables singulation using the 16-DOF Allegro Hand.

We demonstrate extensive experiments in Isaac Gym simulation, showing the ability of our system to singulate a target object in clutter. We directly transfer the policy trained in simulation to the real world.

Over 250 physical robot manipulation trials, our method obtains success rates of 79.2%, outperforming alternative learning and non-learning methods.

---

## Method Overview

This paper introduces a novel approach for robotic object singulation - the process of isolating, grasping, and retrieving a target object from a cluttered environment.

We train a policy in simulation using phase-dependent reward functions. The policy uses the hand joints, the block positions, and the robot arm in the state representation. We directly transfer the trained policy to the real world.

The research presents several key contributions:

1. A framework called Singulating Objects in Packed Environments (SOPE) for training dexterous manipulators to singulate objects in tight spaces.
2. A novel state representation focused on object displacements and a multi-phase reinforcement learning procedure.
3. Extensive simulation experiments in Isaac Gym and real-world validation using an Allegro Hand.

---

## Key Methodological Innovations

### State Representation

{{< image src="images/sopedex/sopedex-staterepresent.webp" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="true" >}}

- Develops a displacement-based state representation that focuses on the target object and its neighbors.
- Uses keypoints to represent object states, reducing the sim-to-real gap compared to image-based representations.
- The representation is scalable and invariant to the total number of objects in the scene.

### Multi-Phase Reinforcement Learning

- Proposes a 3-phase approach: isolating, grasping, and retrieving.
- Each phase has a specific reward function tailored to its objectives.
- This design encourages more robust grasping and lifting behaviors.

### Sim-to-Real Transfer

{{< image src="images/sopedex/sopedex-ComparisonofSim&Real.webp" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="true" >}}

- Achieves zero-shot sim-to-real transfer from Isaac Gym simulation to a physical robot.
- Uses AprilTag markers for accurate state estimation in the real world.
- Employs domain randomization in simulation to enhance robustness.

---

## Experimental Setup

| Setup      | Component        | Details                                            |
| ---------- | ---------------- | -------------------------------------------------- |
| Simulation | Environment      | Isaac Gym (GPU-accelerated reinforcement learning) |
|            | Objects          | Rigid container with rigid blocks                  |
|            | Manipulator      | 16-DOF Allegro Hand                                |
| Real-World | Robot            | Franka Panda arm with Allegro Hand                 |
|            | State Estimation | AprilTag markers on blocks and container           |
|            | Perception       | Two Intel RealSense D435 RGBD cameras              |

## Results

### Simulation Performance

| Method    | 1-out-of-1 | 1-out-of-2 | 1-out-of-5 | 1-out-of-10 |
| --------- | :--------: | ---------: | ---------: | ----------: |
| Tactile   |  .84±.02   |    .84±.02 |    .81±.02 |     .78±.03 |
| Naive     |  .58±.25   |    .57±.27 |    .50±.27 |     .45±.26 |
| Two Phase |  .84±.02   |    .86±.03 |    .81±.03 |     .79±.03 |
| Ours      |  .86±.03   |    .86±.02 |    .82±.02 |     .78±.01 |

- Achieves 86% success rate for singulating 1 out of 1-2 objects.
- Maintains 78% success rate even when singulating 1 out of 10 objects.

### Real-World Performance

| Environment | Method    | Front | Middle-1 | Middle-2 | Back  | Overall | Blocks |
| ----------- | --------- | ----- | -------- | -------- | ----- | ------- | ------ |
| Normal      | Two Phase | 2/15  | 3/15     | -        | 5/15  | 10/45   | 3      |
| Normal      | Ours      | 13/15 | 14/15    | -        | 13/15 | 40/45   | 3      |
| Normal      | S2SS&P    | 10/10 | 6/10     | 10/10    | 10/10 | 36/40   | 4      |
| Normal      | Ours      | 9/10  | 8/10     | 9/10     | 7/10  | 31/40   | 4      |
| Constrained | S2SS&P    | 0/10  | 0/10     | 0/10     | 0/10  | 0/40    | 4      |
| Constrained | Ours      | 7/10  | 6/10     | 5/10     | 10/10 | 28/40   | 4      |

- 88.9% success rate (40/45 trials) for singulating 1 out of 3 objects.
- 77.5% success rate (31/40 trials) for singulating 1 out of 4 objects.
- Demonstrates consistent performance across different block positions (front, middle, back).

---

## Significance and Future Directions

This work represents a significant advancement in dexterous manipulation capabilities for robots, enabling them to handle complex singulation tasks in tightly packed environments. The approach shows promising generalization and robustness, paving the way for more flexible and capable robotic manipulation systems.

Future work could focus on:

- Reducing the real-world engineering required for sim-to-real transfer.
- Extending the approach to handle deformable objects or fragile items.
- Incorporating more sophisticated tactile sensing for enhanced manipulation.

By addressing these challenges, the SOPE framework could lead to robots capable of performing intricate manipulation tasks in diverse real-world scenarios, from warehouse logistics to household assistance.
