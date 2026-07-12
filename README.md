# TCAD Design Optimization of a Scaled 22nm Fully Depleted Silicon-on-Insulator (FD-SOI) NMOS Transistor

## 1. Project Overview

### 1.1 Project Name
22nm FD-SOI Geometry & Mesh Engineering Optimization

### 1.2 Description
* Using Silvaco TCAD (Victory Device), from nanoHUB, the project systematically scales a legacy 50nm baseline design down to a 22nm physical gate length ($L_g$). The primary focus is tracking short-channel degradation phenomena, such as Drain-Induced Barrier Lowering (DIBL) and capacitive charge sharing, and optimizing the physical device layers to reclaim tight electrostatic control over subthreshold transport.

### 1.3 Goals & Objectives
This project aims to:

- Scale a reference 50 nm $L_g$ 2D Silicon-On-Insulator Transistor design down to a 22nm $L_g$ Silicon-On-Insulator Transistor.
- Transition from ideal silicon parameters to realistic sub-micron transport physics by introducing field-dependent mobility degradation models.
- Extract essential baseline transport and parametric characteristics (I-V Curves, Threshold Voltage, Subthreshold Swing, Drain-Induced Barrier Lowering).
- Alter critical structural parameters to see how these characteristics change.

## 2. Requirements
### 2.1 Softwares & Tools
- Silvaco TCAD

### 2.2 Constraints & Challenges
- Ensuring that the device characterizes as intended
- Ensuring no structural gap or overlaps exist, that will cause mesh discontinuity or termination errors during execution.
- Optimize silicon body thickness so that the transistor does not have severe mobility degradation.
- Optimizing the device to have as little DIBL, and have as steep a Subthreshold Swing as possible.


## 3. Development Process
### 3.1 Initial Steps
- 
