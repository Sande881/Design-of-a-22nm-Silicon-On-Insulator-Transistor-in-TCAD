# TCAD Engineering & Design Optimization of a Scaled 22nm Fully Depleted Silicon-on-Insulator (FD-SOI) NMOS Transistor

## 1. Project Overview

### 1.1 Project Name
22nm FD-SOI Geometry & Mesh Engineering Optimization

### 1.2 Description
* This project covers the architectural design, mesh allocation, implementation, and performance debugging of an advanced short-channel Silicon-on-Insulator (SOI) NMOS transistor. Using Silvaco TCAD (Victory Device), the project systematically scales a legacy 50nm baseline design down to a 22nm physical gate length ($L_g$). The primary focus is tracking short-channel degradation phenomena, such as Drain-Induced Barrier Lowering (DIBL) and capacitive charge sharing, and optimizing the physical device layers to reclaim tight electrostatic control over subthreshold transport.

### 1.3 Goals & Objectives
* Symmetric Geometric Scaling: Transition a functional long-channel device blueprint into a scaled 22nm layout spanning an exact $0.122\ \mu\text{m}$ lateral horizontal dimension.
* Electrostatic Recovery: Diagnose structural causes behind an unoptimized subthreshold leakage bottleneck and implement layout parameters to suppress Short-Channel Effects (SCE).
* Target Performance Extraction: Achieve a clean, well-behaved $I_d\text{-}V_g$ transfer characteristic curve with a significantly improved Subthreshold Swing ($SS$) metric.

### 1.4 Key Features
* Localized high-density grid mesh alignment tailored specifically around critical channel-junction boundaries.
* Non-invasive surface-contact metal electrode caps preventing unphysical semiconductor-to-metal region destruction.
* Ultra-Thin Body Fully Depleted SOI (UTB-FD-SOI) channel confinement behavior.

---

## 2. Requirements

### 2.2 Software & Tools
* **Silvaco TCAD Suite (Acqured on nanoHUB)**
  * DeckBuild:Interactive script compiler for writing and processing structured command lines.
  * Victory Device: Advanced multi-dimensional semiconductor physics execution engine.
  * Victory Visual: High-fidelity plotting and analytical scaling visualization utility.

### 2.3 Constraints & Challenges
* Grid Node Allocation Boundaries: Misaligning coordinate declarations risks creating non-physical element gaps or mesh errors during structural initialization.
* Severe Short-Channel Effects (SCE): Reducing the horizontal channel distance without shrinking the vertical junction volume subjects the channel to massive parallel parasitic fields from the drain, completely undermining gate control.
* Modern TCAD Command Compatibility: Eliminating legacy syntax commands (such as avoiding deprecated sweep parameters like `vend`) to prevent terminal execution failure flags.

---

## 3. Development Log

### 3.2 Key Decisions & Changes
* Electrode Position Recess: Shifted the source and drain electrode definitions from bulky 2D interior blocks spanning down to $y=0.02\ \mu\text{m}$ to flat surface caps confined exactly to $y=0.0\ \mu\text{m}$. This preserved the active semiconductor volume for proper high-concentration doping profiles.
* Vertical Channel Volume Reduction: Reduced the physical silicon channel body thickness ($T_{Si}$) from $20\text{ nm}$ ($0.02\ \mu\text{m}$) down to an ultra-thin dimension of **$7\text{ nm}$** ($0.007\ \mu\text{m}$) to force complete charge depletion throughout the film.

### 3.3 Issues & Solutions
* Issue 1: Silicon material definitions unintentionally overwriting the Buried Oxide (BOX) substrate layer due to unbounded region declarations, resulting in vertical silicon short-circuit pillars through the insulation.
  * Solution: Explicitly restructured the bottom-up coordinate sequence hierarchy in Step 2, defining the exact $y$-bounds for both layers independently.
* Issue 2: Executing an electrode statement using named region boundaries directly triggered a `Command Error(null)` terminal prompt.
  * Solution: Removed the invalid string declarations and reverted back to explicit boundary coordinates (`x.min`, `x.max`, `y.min`, `y.max`) combined with positional flags (`top`, `bottom`) to secure clean electrical attachment points.
* Issue 3: The numerical sweep command failed with a `Command Error: Could not find parameter vend` message.
  * Solution: Swapped out the legacy keyword `vend` for the standard, up-to-date parameter name `vfinal=1.2` within the operational gate sweep statement.
* Issue 4: Terminal execution halted with a `/bin/sh: tonyplot: command not found` message.
  * Solution: Acknowledged system path restrictions for legacy visualization wrappers and successfully utilized **Victory Visual** directly to parse layout graphics and export log traces.

---

## 4. Development Process

### 4.1 Iterative Development

#### Phase A: Unoptimized 22nm Device Characterization
* Built the initial 22nm gate length configuration over a standard $20\text{ nm}$ thick silicon body layer.
* Extracted the electrical transfer curve under low drain bias conditions ($V_{drain} = 0.1\text{ V}$).
* Linear and logarithmic visualization traces revealed a highly degraded subthreshold performance slope.

#### Phase B: Ultra-Thin Body (UTB) Optimization
* Adjusted the physical geometry deck to systematically trim down the silicon body layer thickness from $20\text{ nm}$ to a target **$7\text{ nm}$** profile.
* Compiled the updated file through the solver grid arrays, yielding an optimized transfer characteristic response.

#### Calculation of Unoptimized 22nm Device Baseline 
Taking data points from the initial logarithmic sweep:
* Point 1: $V_{g1} = 0.0\text{ V} \rightarrow I_{d1} \approx 6.0 \times 10^{-5}\text{ A}$
* Point 2: $V_{g2} = 0.5\text{ V} \rightarrow I_{d2} \approx 5.5 \times 10^{-4}\text{ A}$

$$SS_{\text{unoptimized}} = \frac{0.5\text{ V} - 0.0\text{ V}}{\log_{10}(5.5 \times 10^{-4}) - \log_{10}(6.0 \times 10^{-5})} \approx \mathbf{520\text{ mV/decade}}$$

* Analysis: The exceptionally wide swing of $520\text{ mV/dec}$ indicates severe Drain-Induced Barrier Lowering (DIBL). The drain's lateral electric field penetrates deep into the thick silicon body, lowering the energy barrier from below and rendering the gate unable to fully shut off the channel.

#### Calculation of Optimized FD-SOI Device Layer
Taking data points from the optimized design run profile:
* Point 1: $V_{g1} = 0.0\text{ V} \rightarrow I_{d1} \approx 6.5 \times 10^{-7}\text{ A}$
* Point 2: $V_{g2} = 0.2\text{ V} \rightarrow I_{d2} \approx 1.0 \times 10^{-5}\text{ A}$

$$SS_{\text{optimized}} = \frac{0.2\text{ V} - 0.0\text{ V}}{\log_{10}(1.0 \times 10^{-5}) - \log_{10}(6.5 \times 10^{-7})} \approx \mathbf{168.5\text{ mV/decade}}$$

* Analysis: Thinning the active body down to a thin 7nm dimension chokes off subterranean leakage paths. The physical volume becomes Fully Depleted, forcing vertical gate field lines to couple tightly through the entire channel down to the buried oxide boundary. This isolates the channel from parasitic lateral drain fields, dramatically sharpening the subthreshold slope down to $168.5\text{ mV/dec}$.


---

## 5. Testing & Validation

### 5.1 Test Cases

| Test Case Name | Expected Result | Actual Result | Status |
| :--- | :--- | :--- | :--- |
| **Material Region Mesh Validation** | Solid, uniform oxide bar running continuously underneath a thin silicon layer. | Pristine horizontal stratification verified with no vertical shorting artifacts. | ✅ |
| **Electrode Placement Boundary Test** | Metal source/drain contact materials restricted strictly to the outer top surface coordinates. | Purple conductor regions properly restricted to surface cap placements without eroding active silicon junctions. | ✅ |
| **Solver Matrix Convergence Test** | Script successfully iterates from gate biases of $0.0\text{ V}$ to $1.2\text{ V}$ without mathematical divergence. | Code deck successfully converges and automatically logs all target current data fields. | ✅ |

### 5.2 Performance & Reliability
Analytical extraction calculations were applied directly to the subthreshold slope characteristics across both engineering design loops:


---
