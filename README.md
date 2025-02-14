# Monte Carlo Simulation for Instrumental Variable Estimation in GAUSS

This repository contains a GAUSS script that implements a Monte Carlo simulation to compare different estimators in both linear and nonlinear models. In particular, the code compares:

- **OLS (Ordinary Least Squares)**
- **2SLS (Two-Stage Least Squares)**
- **IV (Instrumental Variables)**
- **Control Function Approach**

The simulation is run over 100 replications with \(N=1000\) observations per replication.

## Overview

The code is divided into two main sections:

1. **Linear Model & Endogeneity Test**
   - **Data Generation:** Randomly generate explanatory variables \(X1\) and \(X2\) (with \(X2\) being a noisy version of \(X1\)).
   - **Model Specification:** Construct the outcome variables \(Y2\) (the potentially endogenous regressor) and \(Y1\) (the dependent variable) using error terms.
   - **Estimation:**
     - Estimate the model via OLS.
     - Obtain a 2SLS estimate by constructing an instrument matrix after leaving one variable out.
     - Compute an IV estimator directly.
     - Use a control function approach to test for endogeneity by constructing a t-statistic and associated p-value.

2. **Nonlinear Model: 2SLS vs. IV**
   - **Nonlinear Specification:** The model is extended to include a squared term (\(Y2^2\)), and the dependent variable \(Y1\) is modeled as a function of \(X1\), \(Y2\), and \(Y2^2\).
   - **Instrument Construction:**
     - Generate instruments for both \(Y2\) and \(Y2^2\) by regressing these variables on the exogenous variables.
     - Construct the instrument matrix using the estimated coefficients.
   - **Estimation:**
     - Compare OLS, 2SLS, and an “optimal” IV estimator.
     - Store estimates from each replication and, after the loop, compute the median and the median absolute deviation (MAD) of the replicated estimates.

## How to Run

1. **GAUSS Installation:**  
   Make sure you have GAUSS installed on your system.

2. **Running the Code:**  
   Open the GAUSS environment and load and run the script. The results (estimates and test statistics) will be printed to the console.

3. **Output:**  
   - For the linear model, the script prints:
     - OLS, 2SLS, IV, and control function estimates.
     - The p-value from the endogeneity test.
   - For the nonlinear model, after 100 replications, the script prints:
     - The median estimates for OLS, 2SLS, and IV.
     - The median absolute deviations for each estimator.
    
## Discussion
### Data Generation
The code simulates endogenous and exogenous variables. $X_{1}$ is generated from a normal distribution and $X_{2}$ is a noisy copy of $X_{1}$, introducing potential endogeneity in the model.

### Instrument Construction
To address endogeneity, instruments are constructed by deliberately leaving out one variable in the $Y_{2}$-model and then using predicted values to form the instrument matrix.

### Nonlinear Extension
The second part of the simulation extends the model to include a quadratic term, comparing the performance of the different estimators under nonlinearity. The results (medians and MADs) help assess the robustness and efficiency of the estimators.
