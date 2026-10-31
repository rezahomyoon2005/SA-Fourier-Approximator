Function Approximation with Simulated Annealing
A Python/Jupyter Notebook experiment that uses simulated annealing to approximate mathematical functions with a truncated Fourier series. The notebook explores how the initial temperature, cooling rate, and perturbation size affect optimization.

Overview
Instead of calculating Fourier coefficients analytically, this project treats them as an optimization problem. Simulated annealing searches for coefficients that minimize the root mean squared error (RMSE) between a target function and the Fourier approximation over sampled points.

The approximation takes the form

𝑓
^
(
𝑥
)
=
𝑎
0
2
+
∑
𝑛
=
1
20
(
𝑎
𝑛
cos
⁡
(
𝑛
𝑥
)
+
𝑏
𝑛
sin
⁡
(
𝑛
𝑥
)
)
.
f
^
​
 (x)= 
2
a 
0
​
 
​
 + 
n=1
∑
20
​
 (a 
n
​
 cos(nx)+b 
n
​
 sin(nx)).
A candidate solution is a 41-dimensional vector: 21 cosine/constant coefficients and 20 sine coefficients.

How It Works
Select a target function and generate samples over [-π, π].
Initialize the 41 Fourier coefficients randomly.
Generate a neighboring solution by perturbing three randomly chosen coefficients.
Calculate the RMSE of the new approximation.
Accept improvements, or sometimes accept worse solutions according to the simulated annealing acceptance rule.
Decrease the temperature by multiplying it by the cooling factor alpha after each iteration.
Return the best coefficients found and plot the target function against its approximation.
The notebook includes the following main functions:

Function	Purpose
getTargetFunction()	Returns one of the supported mathematical target functions
cost_func()	Computes RMSE for a candidate coefficient vector
next_state()	Perturbs three randomly selected coefficients
simulated_annealing()	Runs the optimization and tracks the best solution
Simulated_annealing()	Sets up the experiment and visualizes the fitted function
Supported Target Functions
The target-function selector includes:

Sine/cosine combination (sin_cos)
Linear (linear)
Quadratic (quadratic)
Cubic (cubic)
Gaussian (gaussian)
Square wave (square_wave)
Sawtooth (sawtooth)
Multi-frequency Fourier combination (complex_fourier)
Polynomial (polynomial)
Not all of these options are run in the saved notebook; they are available for additional experiments.

Parameters
Argument	Description
func_name	Target function to approximate
A_star	Range used to initialize coefficients between -A_star and A_star
sample_size	Number of sample points
T	Initial temperature
sigma	Magnitude of random coefficient perturbations
alpha	Temperature multiplier per iteration
max_iter	Number of optimization iterations
Note: In the current implementation, next_state() clips proposed coefficients to [-10, 10], regardless of A_star. Also, three coefficient positions are updated per move.

Experiments
The notebook tests several target functions and examines how temperature affects the approximation. Saved experiments include:

Target / experiment	Initial temperature	sigma	alpha	Iterations
Sine/cosine	10,000	0.5	0.95	3,000
Linear	100	0.5	0.99	3,000
Quadratic	10,000	0.4	0.99	5,000
Sawtooth	8,000	0.25	0.96	3,500
Sawtooth — very high temperature	1,000,000	0.5	0.99	3,000
Sawtooth — very low temperature	0.0003	0.7	0.98	2,000
The notebook prints optimization progress every 100 iterations and plots the target function alongside the Fourier approximation. The saved runs demonstrate that approximation quality and convergence behavior depend strongly on the chosen settings. These are individual stochastic runs, not a systematic benchmark across repeated random seeds.

Getting Started
Requirements
Python 3
NumPy
Matplotlib
Jupyter Notebook (or Kaggle/Google Colab)
Install the necessary libraries locally:

pip install numpy matplotlib notebook
Run the Notebook
Open simulated_ann.ipynb in Jupyter, Kaggle, or Colab.
Run the definition cells first.
Execute an experiment cell to view the optimization log and comparison plot.
Change the target function or parameters to compare different configurations.
For example:

optimal_state, errors = Simulated_annealing(
    "sin_cos",
    A_star=10,
    sample_size=200,
    T=10000,
    sigma=0.5,
    alpha=0.95,
    max_iter=3000
)
Observations and Limitations
A high temperature permits more exploration, while cooling makes the search more selective.
The fixed 20-harmonic Fourier approximation may not represent every target function equally well, especially functions with discontinuities or strong nonperiodic behavior over the chosen interval.
Optimization is stochastic: different runs can produce different coefficients and errors.
Temperature may become extremely small during long runs, so a temperature floor or stopping criterion could improve numerical robustness.
The current clipping range in next_state() is fixed rather than linked to the initialization parameter A_star.
Some notebook headings and experiment calls do not correspond exactly (for example, a cell under cubic runs sawtooth); consult the function arguments to identify what was actually tested.
Possible Improvements
Compare multiple runs using different random seeds and report average RMSE.
Plot RMSE against iteration for each experiment using the returned errors list.
Test alternative cooling schedules and adaptive perturbation sizes.
Make the coefficient bounds consistent between initialization and neighbor generation.
Add automated comparisons against analytical or least-squares Fourier fitting.
Technologies
Python · NumPy · Matplotlib · Jupyter Notebook
