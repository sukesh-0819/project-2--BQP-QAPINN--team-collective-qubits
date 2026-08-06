# WISER Quantum Challenge 2026: Quantum Assisted Physics-Informed Neural Networks for CFD

**Team Name:** Collective Qubits  
**Team Members:** Sukesh Nasinaa,Padmavathi A, Shashank  
**Project:** BQP Challenge Submission  

---

## 📌 Project Overview
Physics-Informed Neural Networks (PINNs) are powerful tools for solving partial differential equations (PDEs) by embedding physical laws directly into the network architecture, bypassing the need for explicit grid generation. However, classical PINNs (c-PINNs) face significant limitations when solving high-dimensional, non-linear PDEs. They often suffer from parameter explosion, slow evaluation times, and spectral bias, which causes them to smooth out sharp, high-frequency transitions (like shockwaves) and stall in local minima.

This project introduces **Quantum-Assisted Physics-Informed Neural Networks (QAPINNs)** to overcome these limitations. By embedding a Variational Quantum Circuit (VQC) into the architecture, we drastically reduce the trainable parameter count while leveraging quantum entanglement to coordinate spatio-temporal updates in Hilbert space.

---

## 📂 Repository Structure & Deliverables

```text
.
├── report/              # Comprehensive Technical Report (PDF) detailing methodology, XAI, and spectral analysis
├── src/                 # Source code containing c-PINN baseline and QAPINN implementations
├── xai_visualizations/  # Scripts and output images for XAI mapping, gradient flow, and loss landscapes
├── presentation/        # Presentation slides summarizing findings for the judging panel
└── README.md            # Reproducibility instructions and summary of findings (this document)


📐 Mathematical FormulationOur models are trained and evaluated on fundamental fluid and thermal dynamics equations:1D Viscous Burgers' Equation:$$\frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} = \nu \frac{\partial^2 u}{\partial x^2}$$1D Heat Equation:$$\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}$$Models are trained using a composite Mean Squared Error (MSE) loss function ($\mathcal{L}_{\text{total}}$) that balances PDE residual loss, initial condition loss, and boundary condition loss. Performance is evaluated using the relative $L_2$ error metric to measure global pointwise accuracy against the exact analytical solution.⚛️ QAPINN Architecture & MethodologyOur hybrid QAPINN architecture modifies a standard 4-layer classical network (50 neurons per layer, Tanh activation) by replacing the third hidden layer with a parameterized quantum layer.Key design choices for the quantum layer include:Ansatz: We utilize a Cascade Ansatz. Comparative analysis against cross-mesh, alternate, and strongly entangled topologies proved that the cascade configuration yielded the best loss convergence relative to its circuit depth and parameter count.Encoding: We use Angle Embedding ($RX$ gates) rather than amplitude encoding. Angle embedding acts naturally as a partial Fourier series, making it vastly superior for fitting the smooth differential equations and oscillatory patterns required in PINNs.Measurement: Features are extracted using Pauli-$Z$ expectation values rather than probability state vectors, ensuring efficient classical post-processing.Optimization: Optimized using Adam with a learning rate of $0.005$, paired with a ReduceLROnPlateau scheduler. Models were trained for 12,000 to 15,000 epochs.📈 Summary of Key FindingsData Efficiency: The classical PINN required a dense dataset of 25,600 collocation points to achieve an acceptable $L_2$ error. The QAPINN achieved comparable accuracy using only 2,500 uniformly distributed points.Parameter Reduction: Placing the VQC as the third hidden layer drastically reduced the number of trainable parameters in that layer to just 563, accelerating run times and lowering memory footprint.Mitigation of Spectral Bias: Spatial Fast Fourier Transform (FFT) analysis confirmed that classical DNNs struggle to capture high-frequency details. The QAPINN successfully resolves high-wavenumber components ($|k| > 10$) over time via expressive Hilbert-space mappings.Noise Reduction: At the initial temporal state, the QAPINN exhibited a clean, noise-free high-frequency tail, avoiding spurious high-wavenumber oscillations present in the classical baseline.👥 Team & Individual ContributionsSukesh: Developed and implemented the PyTorch–PennyLane QAPINN and c-PINN codebase, conducted comparative performance analysis across multi-qubit circuit topology variants, and evaluated loss trajectories.Padmavathi A: Researched Explainable AI (XAI) frameworks for hybrid quantum-classical networks, authored diagnostic scripts for gradient flow tracking and loss decoupling, and mapped spatial-temporal error fields.Shashank: Conducted literature survey and background review, designed and executed Fast Fourier Transform (FFT) dynamic spectral analysis scripts, and analyzed high-wavenumber mode resolution.
