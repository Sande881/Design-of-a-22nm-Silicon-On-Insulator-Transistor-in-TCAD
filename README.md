# TCAD Design Optimization of a Scaled 22nm Fully Depleted Silicon-on-Insulator (FD-SOI) NMOS Transistor

## 1. Project Overview

### 1.1 Project Name
22nm FD-SOI Geometry & Mesh Engineering Optimization

### 1.2 Description
Silicon on Insulator (SOI) technology consists of a layered structure where a thin silicon layer is separated from the bulk silicon substrate by an insulating layer. This insulating layer, often made of silicon dioxide, is crucial for minimizing parasitic capacitance, which can hinder the performance of electronic devices. Fully Depleted refers to the use of the entire thickness of the silicon layer is used as the channel, which means that it does not require channel doping due to the channel layer being very thin.

<img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/54dd21ca-cd86-4999-a87e-c7054f45b2bd" />

(source of image: https://www.slideshare.net/slideshow/silicon-on-insulator-soi-technology/83737859)


Using Silvaco TCAD (Victory Device), from nanoHUB, the project systematically scales a legacy 50nm baseline design down to a 22nm physical gate length ($L_g$) Fully-Depleted Silicon-On-Insulator. The primary focus is tracking short-channel degradation phenomena, such as Drain-Induced Barrier Lowering (DIBL) and capacitive charge sharing, and optimizing the physical device layers to reclaim tight electrostatic control over subthreshold transport.

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
We start by launching Victory TCAD Lab via nanoHUB, and run a script for a reference 2D Silicon-On-Insulator NMOS Transistor of 50 nm of Gate Length ($L_g$) and 5 nm silicon channel thickness. This is our base, which we optimize to get our intended final device.

#### Structure:
<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/e1469e37-3b6f-4f6c-8bb7-55c52c66e573" />

#### Doping Profile:
<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/2950ce2a-b034-417e-8cb6-4d0da957bd43" />

#### I<sub>d</sub>-V<sub>g</sub> Plots

<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/1c99ed83-22d3-43bd-a3b8-3d1b546c9cdf" />

* Log I<sub>d</sub>-V<sub>g</sub> Plot:
<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/f31d7fbe-0254-4716-90d7-6794c4f2e781" />

* Low and High Drain Bias Log I<sub>d</sub>-V<sub>g</sub> Plot:

<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/9f39817b-eda7-4f55-96b8-aee80bca0065" />



#### Parameters:

- I<sub>on</sub> = 5.7374 x 10<sup>-4</sup> A 
- I<sub>off</sub> = 2.18297 x 10<sup>-10</sup> A
- $$\frac{I_on}{I_off}$$ = 2.620691 x 10<sup>6<sup>
- Threshold Voltage(V<sub>th</sub>) at Linear Bias = 0.260 V
- Threshold Voltage(V<sub>th</sub>) at Saturation Bias = 0.210 V
- Subthreshold Swing (SS) = $$\frac{\Delta V_G}{\Delta \log_{10}(I_D)}$$ = 81.59 mV/dec
- Drain-Induced Barrier Lowering (DIBL) = 55.94 mV/V

## 3.2 Development
With our base parameters established, we now scale down the gate length to 22 nm. Retaining the original 5 nm of body thickness will result in poor electrostatic control, causing severe short-channel effects and degrading our subthreshold swing, thus we will scale it down to 3 nm of body thickness. We tighten our oxide thickness to 1.5 nm so that the gate retains dominant control over the channel, and increase our doping concentration to drain's depletion region from punching straight through to the source.

## Structure:
<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/ac662c27-c471-4fac-8b4d-f8edd0e43a3b" />

#### Doping Profile:
<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/332abf11-5448-4a9e-8f2e-ca1a2e189a67" />

#### I<sub>d</sub>-V<sub>g</sub> Plots
<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/36eb994b-5ba5-4b45-acbb-67e3cb700ea3" />

* Log I<sub>d</sub>-V<sub>g</sub> Plot:

<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/bf4a9d02-a9d3-4235-a914-5d04ec2efecf" />


* Low and High Drain Bias Log I<sub>d</sub>-V<sub>g</sub> Plot:

#### Parameters:

- I<sub>on</sub> = 5.22214 x 10<sup>-4</sup> A 
- I<sub>off</sub> = 8.53338 x 10<sup>-13</sup> A
- $$\frac{I_on}{I_off}$$ = 6.1196619 x 10<sup>8<sup>
- Threshold Voltage(V<sub>th</sub>) at Linear Bias =  V
- Threshold Voltage(V<sub>th</sub>) at Saturation Bias =  V
- Subthreshold Swing (SS) = $$\frac{\Delta V_G}{\Delta \log_{10}(I_D)}$$ =  mV/dec
- Drain-Induced Barrier Lowering (DIBL) =  mV/V



### Comparison of 3 nm vs 5 nm body thickness :


### Key Decisions & Changes
- Added Light-Doped Drain
- Added Dielectric sidewalls
- Put high-k dielectric Hafnium Oxide (HfO2) for Gate Oxide

### Issues & Solutions
- **Issue:** *Describe the problem.*
  - **Solution:** *Describe how it was solved.*



  
  


