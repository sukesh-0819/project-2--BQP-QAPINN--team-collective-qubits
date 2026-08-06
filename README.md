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
