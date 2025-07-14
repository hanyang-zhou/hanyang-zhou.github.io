---
title: "Introducing the MOTIF Hand: A Revolutionary Multimodal Robotic Hand for Advanced Manipulation"
meta_title: "MOTIF Hand"
description: "We present the MOTIF Hand, a novel multimodal robotic hand that integrates thermal, inertial, and force sensors for enhanced dexterous manipulation capabilities."
date: 2025-07-13T05:00:00Z
image: "images/motif/motif-hand-overview.png"
categories: ["Research"]
author: "Hanyang ZHOU"
tags: ["Dexterous Hand", "Multimodal Sensing", "Robotics", "Thermal Sensing"]
draft: false
---

This paper presents the **MOTIF Hand (Multimodal Observation with Thermal, Inertial, and Force sensors)**, a groundbreaking robotic hand that extends the LEAP hand design with comprehensive multimodal sensing capabilities including dense tactile information, thermal imaging, depth sensing, and inertial measurement units.

We hope this work can demonstrate remarkable versatility in complex manipulation tasks, enabling temperature-aware grasping and mass discrimination through simple interactions, opening new possibilities for safer and more intelligent robotic manipulation.

{{< accordion "Where can you find MORE interseting videos?" >}}

**Check our presentation slides on** [YouTube Channel](https://youtu.be/9-12XRvFEbU), **See more details on our** [Project Website](https://slurm-lab-usc.github.io/motif-hand).

{{< /accordion >}}

## About this Project

Dexterous manipulation using multi-fingered robotic hands has advanced rapidly in recent years, but existing systems predominantly rely on vision and basic tactile sensing. This limitation becomes particularly challenging in real-world scenarios that require reasoning about multiple sensing modalities or operating in environments where vision alone is insufficient.

In this work, we introduce the MOTIF Hand, which addresses these limitations by integrating multiple sensing modalities into a single, cohesive platform. Built upon the proven LEAP hand architecture, our system incorporates thermal imaging, depth sensing, dense tactile arrays, and inertial measurement units to create one of the most comprehensive multimodal hands available today.

We demonstrate the system's capabilities through two key experiments: temperature-aware safe grasping using thermal-guided manipulation policies, and mass classification through fingertip \"flick\" interactions that leverage multimodal sensor fusion.

---

## Method Overview

The MOTIF Hand represents a significant step forward in robotic sensing technology, combining multiple sensing modalities in a unified, low-cost platform designed for practical deployment.

Our approach centers on extending the LEAP hand with carefully integrated sensor arrays while maintaining the system's affordability and reproducibility. The hand features a three-tier processing architecture that efficiently manages data from diverse sensing modalities and enables real-time multimodal perception.

The research presents several key contributions:

1. A comprehensive multimodal robotic hand that integrates thermal, tactile, depth, and inertial sensing in a single platform.
2. Novel applications demonstrating temperature-aware manipulation and mass discrimination through multimodal sensor fusion.
3. A cost-effective design (under $4000 USD) that maintains reproducibility for widespread adoption.

---

## Key Methodological Innovations

### Multimodal Sensor Integration

{{< image src="images/motif/motif-sensor-layout.png" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

- **Thermal Sensing**: FLIR Lepton 3.5 thermal camera provides 160×120 resolution infrared temperature data, upscaled to 1080×960 through interpolation
- **Tactile Arrays**: Thin film pressure sensors across finger pads with 6×6 sampling precision at 2.5mm resolution
- **Depth Perception**: Time-of-flight sensor provides real-time distance measurements from palm to contact surfaces
- **Inertial Measurement**: 9-axis IMU sensors at each finger joint combining accelerometer, gyroscope, and magnetometer data
- **Visual Input**: High-resolution RGB camera at 30fps for visual context

### Three-Tier Processing Architecture

- **First Tier**: Individual finger joint processing units with motion tracking and electromagnetic interference shielding
- **Second Tier**: Palm-based data integration module using RS485 serial communication and Modbus protocol
- **Third Tier**: Raspberry Pi 5 for high-level multimodal data fusion and real-time processing

### Temperature-Aware Manipulation Pipeline

{{< image src="images/motif/motif-thermal-pipeline.png" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

- Develops a \"Real2Sim\" pipeline that uses thermal and RGB data to build geometric and thermal object representations
- Employs Structure-from-Motion and Gaussian Splatting for dense 3D reconstruction
- Implements thermal-RGB alignment using SIFT correspondences and reprojection techniques
- Creates thermal affordance maps for safe grasping policy generation

---

## Experimental Setup

| Component       | Specification         | Details                                 |
| --------------- | --------------------- | --------------------------------------- |
| Base Platform   | LEAP Hand             | 16-DOF dexterous manipulation platform  |
| Thermal Camera  | FLIR Lepton 3.5       | 160×120 native, 1080×960 interpolated   |
| Tactile Sensors | Thin Film Arrays      | 6×6 grid, 2.5mm resolution, 20g trigger |
| IMU Sensors     | 9-Axis Units          | BMM350 magnetic sensor with shielding   |
| Depth Sensor    | ToF Module            | Real-time palm-to-surface distance      |
| RGB Camera      | Raspberry Pi Module 3 | 30fps high-resolution imaging           |
| Processing      | Raspberry Pi 5        | Enhanced computational power            |
| Cost            | Under $4000 USD       | Accessible and reproducible design      |

## Results

### Temperature-Aware Safe Grasping

{{< image src="images/motif/motif-grasping.png" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

The thermal-guided manipulation experiment demonstrates the system's ability to safely handle objects with temperature variations:

- **3D Thermal Mapping**: Successfully reconstructed thermal affordance maps from multimodal sensor data
- **Safe Grasp Planning**: Developed policies that avoid high-temperature regions while maintaining stable grasps
- **Real2Sim Transfer**: Achieved effective sim-to-real policy transfer using thermal-geometric object models
- **Denoising Pipeline**: Implemented robust thermal data processing to handle sensor noise and artifacts

The system successfully avoided grasping hot regions on objects while maintaining manipulation effectiveness, demonstrating practical safety capabilities for real-world deployment.

### Multimodal Mass Classification

{{< image src="images/motif/motif-mass-classification.png" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

The fingertip "flick" experiment showcased the hand's ability to distinguish objects by mass through dynamic interaction:

| Object         | Mass | Classification Accuracy       |
| -------------- | ---- | ----------------------------- |
| Red U-Shape    | 82g  | High displacement detection   |
| Blue U-Shape   | 125g | Medium displacement detection |
| Purple U-Shape | 219g | Low displacement detection    |

- **Feature Extraction**: Derived 42 statistical features from accelerometer, gyroscope, and magnetometer data
- **Linear Discriminant Analysis**: Achieved strong class separation with 77.5% variance explained by first discriminant
- **Physical Interpretation**: Acceleration-based features (ACC_Z_Min: 49.48, ACC_Range: 47.98) provided primary discrimination
- **Real-time Performance**: 2ms update intervals with 115200 baud rate data transmission

The LDA analysis revealed distinct clustering of mass categories with minimal overlap, demonstrating the system's capability to infer physical properties through brief contact interactions.

{{< image src="images/motif/motif-mass-classification-result.png" caption="" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

---

## Learning by Feeling: A Developmental Perspective

Just as human infants learn to navigate the world through rich multisensory exploration, we believe robotic manipulation is currently in its early developmental stages. Like babies taking their first steps, current manipulation policies are akin to curious children exploring a new world, trying different ways to sense and understand everything around them.

We are still in the phases of skill acquisition and exploration, moving toward what we hope will eventually become convergence and evolution in robotic dexterity. The multimodal sensing capabilities we present could complement the currently dominant visual input or even bypass many of its fundamental limitations. Some challenges may require entirely new framework designs, while others can potentially be solved through better sensing architectures like the MOTIF Hand.

**Key Impact Areas:**

- **Cooking and Food Handling**: Thermal sensing enables safe interaction with hot surfaces and temperature-sensitive materials, replicating human thermal perception that detects heat before physical contact occurs
- **Industrial Applications**: Enhanced safety for welding, hot metal handling, and quality control processes where temperature awareness is critical
- **Material Classification**: Multimodal sensing allows robots to distinguish object textures and material properties through contact, expanding beyond vision-only approaches
- **Healthcare and Assistance**: Safer human-robot interaction through comprehensive temperature and force monitoring
- **Research Platform**: The comprehensive sensor suite enables investigation of multimodal manipulation strategies previously impossible with traditional systems

### Future Research Directions

Our vision extends well beyond the current capabilities, focusing on several key areas:

**Real-time Thermal-Aware Manipulation Enhancement:**

- Integrate point cloud-based SLAM with thermal distribution mapping for dynamic environment understanding
- Develop real-time temperature perception that can be seamlessly plugged into standard manipulation pipelines
- Create thermal affordance maps that update continuously during manipulation tasks

**Advanced Multimodal Fusion:**

- Explore sophisticated algorithms that leverage all sensing modalities simultaneously rather than in isolation
- Investigate how different sensor combinations can compensate for individual sensor limitations
- Develop learning frameworks that can adapt sensor fusion strategies based on task requirements

**Platform Evolution:**

- Integration of fingertip sensors such as Digit 360 for enhanced tactile resolution at contact points
- Extension to soft-skinned versions following LEAP Hand v2 developments for more anthropomorphic interaction
- Expansion to additional sensing modalities as new technologies become available

**A Vision for the Future:**
Multi-modal sensing is not just an enhancement to current robotic capabilities—it is essential for real-world manipulation and robot-environment interaction. As we direct the field's steps from its current exploratory phase toward maturity, platforms like the MOTIF Hand serve as stepping stones toward robots that can truly understand and interact with the rich, complex world around them.

The ultimate goal is developing robots capable of sophisticated, intuitive manipulation in diverse real-world scenarios, from delicate cooking tasks to robust industrial operations, all while maintaining the safety and adaptability that comes from comprehensive environmental awareness.
