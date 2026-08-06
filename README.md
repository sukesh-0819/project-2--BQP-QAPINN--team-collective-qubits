# WISER Quantum Challenge 2026: Quantum Assisted Physics-Informed Neural Networks for CFD

**Team Members:** Sukesh Nasina,Padmavathi A, Shashank  
**Project:** BQP Challenge Submission  

---

## Project Overview
Physics-Informed Neural Networks (PINNs) are powerful tools for solving partial differential equations (PDEs) by embedding physical laws directly into the network architecture, bypassing the need for explicit grid generation. However, classical PINNs (c-PINNs) face significant limitations when solving high-dimensional, non-linear PDEs. They often suffer from parameter explosion, slow evaluation times, and spectral bias, which causes them to smooth out sharp, high-frequency transitions (like shockwaves) and stall in local minima.

This project introduces Quantum-Assisted Physics-Informed Neural Networks (QAPINNs) to overcome these limitations. By embedding a Variational Quantum Circuit (VQC) into the architecture, we drastically reduce the trainable parameter count while leveraging quantum entanglement to coordinate spatio-temporal updates in Hilbert space.

---

## Challenge Deliverables & Repository Structure
* **report/:** Contains the comprehensive Technical Report (PDF) detailing our methodology, XAI metrics, and spectral analysis.
* **src/:** The source code repository containing both the c-PINN baseline and the QAPINN implementations.
* **xai_visualizations/:** Scripts and output images for our Explainable AI (XAI) mapping, gradient flow tracking, and decoupled loss landscapes.
* **presentation/:** The presentation slides summarizing our findings for the judging panel.
* **README.md:** Reproducibility instructions and summary of key findings (this document).

---

## Mathematical Formulation
Our models are trained and evaluated on fundamental fluid and thermal dynamics equations:

**1D Viscous Burgers' Equation:**
$$\frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} = \nu \frac{\partial^2 u}{\partial x^2}$$

Models are trained using a composite Mean Squared Error (MSE) loss function ($\mathcal{L}_{\text{total}}$) that balances PDE residual loss, initial condition loss, and boundary condition loss. Performance is evaluated using the relative $L_2$ error metric to measure global pointwise accuracy against the exact analytical solution.

---

## QAPINN Architecture & Methodology
Our hybrid QAPINN architecture modifies a standard 4-layer classical network (50 neurons per layer, Tanh activation) by replacing the third hidden layer with a parameterized quantum layer.

Key design choices for the quantum layer include:

* **Ansatz:** We utilize a Cascade Ansatz. Comparative analysis against cross-mesh, alternate, and strongly entangled topologies proved that the cascade configuration yielded the best loss convergence relative to its circuit depth and parameter count.
* **Encoding:** We use Angle Embedding (RX gates) rather than amplitude encoding. Angle embedding acts naturally as a partial Fourier series, making it vastly superior for fitting the smooth differential equations and oscillatory patterns required in PINNs.
* **Measurement:** Features are extracted using Pauli-Z expectation values rather than probability state vectors, ensuring efficient classical post-processing.
* **Optimization:** The network is optimized using Adam with a learning rate of 0.005, paired with a ReduceLROnPlateau scheduler. Models were trained for 12,000 to 15,000 epochs.

---


## Summary of Key Findings
* **Data Efficiency:** The classical PINN required a dense dataset of 25,600 collocation points to achieve an acceptable $L_2$ error. The QAPINN achieved comparable accuracy using only 2,500 uniformly distributed points, demonstrating vastly superior data efficiency.
* **Parameter Reduction:** Placing the VQC as the third hidden layer drastically reduced the number of trainable parameters in that layer to just 563, accelerating run times and lowering the memory footprint.
* **Mitigation of Spectral Bias:** Spatial Fast Fourier Transform (FFT) analysis confirmed that classical DNNs struggle to capture high-frequency details. The QAPINN successfully resolves high-wavenumber components ($|k| > 10$) over time, driven by the expressive multi-frequency Hilbert-space mappings of the quantum angle embedding.
* **Noise Reduction:** At the initial temporal state, the QAPINN exhibited a completely clean, noise-free high-frequency tail, avoiding the spurious high-wavenumber oscillations present in the classical baseline.

---

## 👥 Team & Individual Contributions

* **Sukesh**: Developed and implemented the core PyTorch–PennyLane hybrid network architecture, conducted comparative experimental benchmarking across circuit ansatzes and qubit configurations, and performed parameter and loss convergence analyses.
* **Padmavathi A**:  Researched Explainable AI (XAI) frameworks for hybrid quantum-classical networks, authored the diagnostic codebase, and
generated loss component decoupling and gradient flow visualizations.
* **Shashank**: Conducted the initial literature survey and theoretical background review, designed and executed the Fast Fourier Transform (FFT)
dynamic spectral analysis, and analyzed high-frequency mode capturing.
---

## Reproducibility & Execution Instructions
To replicate the results presented in our technical report, follow these steps:

1. Clone this repository to your local machine or compute node.
2. Ensure you have a Python 3.8+ environment active.
3. Install the required dependencies (including PyTorch and PennyLane) by running: `pip install -r requirements.txt`
4. To train the classical baseline PINN, navigate to the src directory and execute: `python train_cpinn.py`
5. To train the Quantum-Assisted PINN using the optimized cascade ansatz, execute: `python train_qapinn.py`
6. To generate the Spectral Analysis and XAI Heatmaps, run: `python generate_xai_plots.py`
