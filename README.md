# TCAD Design Optimization of a Scaled 22nm Fully Depleted Silicon-on-Insulator (FD-SOI) NMOS Transistor

## 1. Project Overview

### 1.1 Project Name
22nm FD-SOI Geometry & Mesh Engineering Optimization

### 1.2 Description
* Silicon on Insulator (SOI) technology consists of a layered structure where a thin silicon layer is separated from the bulk silicon substrate by an insulating layer. This insulating layer, often made of silicon dioxide, is crucial for minimizing parasitic capacitance, which can hinder the performance of electronic devices. Fully Depleted refers to the use of the entire thickness of the silicon layer is used as the channel, which means that it does not require channel doping due to the channel layer being very thin.

<img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/54dd21ca-cd86-4999-a87e-c7054f45b2bd" />

(source of image: https://www.slideshare.net/slideshow/silicon-on-insulator-soi-technology/83737859)


* Using Silvaco TCAD (Victory Device), from nanoHUB, the project systematically scales a legacy 50nm baseline design down to a 22nm physical gate length ($L_g$) Fully-Depleted Silicon-On-Insulator. The primary focus is tracking short-channel degradation phenomena, such as Drain-Induced Barrier Lowering (DIBL) and capacitive charge sharing, and optimizing the physical device layers to reclaim tight electrostatic control over subthreshold transport.

### 1.3 Goals & Objectives
This project aims to:

- Scale a reference 50 nm $L_g$ 2D Silicon-On-Insulator Transistor design down to a 22nm $L_g$ Silicon-On-Insulator Transistor.
- Transition from ideal silicon parameters to realistic sub-micron transport physics by introducing field-dependent mobility degradation models.
- Extract essential baseline transport and parametric characteristics (I-V Curves, Threshold Voltage, Subthreshold Swing, Drain-Induced Barrier Lowering).
- Alter critical structural parameters to see how these characteristics change.

## 2. Requirements
### 2.1 Softwares & Tools
- Silvaco TCAD (Victory TCAD)

### 2.2 Constraints & Challenges
- Ensuring that the device characterizes as intended, working as per the required calculations.
- Ensuring no structural gap or overlaps exist, that will cause mesh discontinuity or termination errors during execution.
- Optimize silicon body thickness so that the transistor does not have severe mobility degradation.
- Optimizing the device to have as little DIBL, and have as steep a Subthreshold Swing as possible.


## 3. Development Process
### 3.1 Initial Steps
We start by launching Victory TCAD Lab via nanoHUB, and run a script for a reference 2D Silicon-On-Insulator NMOS Transistor of 50 nm of Gate Length ($L_g$) and 7 nm silicon channel thickness. The script shall be written as such:



Now we get the following,

* Structure:

  
  


