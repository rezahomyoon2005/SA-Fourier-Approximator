
---

# 📈 Function Approximation using Simulated Annealing & Fourier Series

This project demonstrates the power of the **Simulated Annealing (SA)** algorithm in finding optimal coefficients for **Fourier Series** to approximate various mathematical functions.

## 📝 Project Overview

Approximating complex functions is a fundamental task in numerical analysis and signal processing. This repository provides a Python implementation that uses the Simulated Annealing metaheuristic to minimize the Root Mean Square Error (RMSE) between a target function and its Fourier approximation.

### Supported Target Functions:

The objective is to find the best matching coefficients for:

* **Periodic Functions:** Sine + Cosine, Complex Fourier.
* **Linear & Polynomial:** Linear, Quadratic, Cubic, and high-degree Polynomials.
* **Special Functions:** Gaussian, Square Wave, and Sawtooth Wave.

## 🛠️ Key Features

* **Optimization Engine:** Custom implementation of the Simulated Annealing algorithm with adaptive cooling schedules.
* **Fourier Series:** Uses 20 harmonics (41 coefficients in total) to represent complex signals.
* **Dynamic Perturbation:** The `next_state` function intelligently explores the search space by applying random noise to coefficients.
* **Visualization:** Real-time plotting of the Target Function vs. the Fourier Approximation to see the convergence quality.

## 🚀 How It Works

1. **Initialization:** Starts with random coefficients for the Fourier series.
2. **Cost Evaluation:** Calculates the **RMSE** between the actual function samples and the estimated values.
3. **Search & Acceptance:** In each iteration, it explores neighboring solutions. If a new set of coefficients is better, it's accepted. If worse, it may still be accepted based on the "Temperature" to avoid local minima.
4. **Cooling:** The temperature decreases over time (`T *= alpha`), narrowing the search toward the global optimum.

## 📦 Requirements

To run this notebook, you need the following Python libraries:

* `numpy`
* `matplotlib`

```bash
pip install numpy matplotlib

```

## 📊 Results

The algorithm successfully fits various waveforms. Below is an example of the convergence log:

* **Initial Cost:** ~26.75
* **Final Cost (after 3000 iterations):** ~0.49
* **Efficiency:** Shows a smooth transition from exploration to fine-tuning.

---

*Developed as part of a series of 7 computational projects.*

---

