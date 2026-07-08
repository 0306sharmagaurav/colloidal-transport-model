# Colloidal Transport Modelling and Parameter Estimation

## Project Overview

This project implements a computational model to simulate the transport of microplastic particles through saturated porous media and estimate the governing transport parameters by fitting the model to experimental breakthrough curve (BTC) data.

Rather than focusing only on reproducing experimental observations, the project emphasizes the numerical implementation of transport equations, parameter estimation, and optimization. The model was developed incrementally to understand the contribution of each physical process before replacing manual parameter tuning with automated optimization using Differential Evolution.

The project was carried out as part of a summer research internship, where the experimental problem served as the motivation for developing the computational model.

---

## Problem Statement

Predicting particle transport through porous media requires solving coupled transport equations containing several unknown parameters. Since these parameters cannot be measured directly from breakthrough curves, they must be estimated through inverse modelling.

The objective of this project was to:

- develop a numerical transport model from first principles,
- incorporate the major particle retention mechanisms,
- compare simulated and experimental breakthrough curves, and
- automate parameter estimation using numerical optimization instead of manual trial-and-error.

---

## Methodology

The project was developed in stages to understand the computational effect of each transport mechanism before combining them into a single model.

### 1. Tracer Transport

Implemented a one-dimensional Advection-Dispersion Equation (ADE) to simulate conservative tracer transport and understand the influence of advection and dispersion on breakthrough behaviour.

### 2. Attachment

Added first-order particle attachment to represent irreversible deposition on collector surfaces and studied its effect on outlet concentration.

### 3. Detachment

Introduced reversible particle release to simulate remobilization of previously retained particles and analyze its influence on breakthrough curve tailing.

### 4. Blocking

Implemented Langmuir-type blocking to account for the finite availability of attachment sites and investigate its effect on particle retention.

### 5. Straining

Extended the model by introducing particle straining as an additional retention mechanism. The implementation was further modified to allow depth-dependent straining through an exponentially varying straining coefficient.

### 6. Parameter Estimation

Initially, model parameters were explored manually to understand the physical role of each process and its effect on the simulated breakthrough curve.

After establishing these relationships, manual tuning was replaced by Differential Evolution optimization, allowing simultaneous estimation of:

- Attachment efficiency (α)
- Detachment coefficient (kdet)
- Straining coefficient (kstr0)
- Depth dependency coefficient (β)
- Maximum attachment capacity (Smax)

The objective function minimized the Root Mean Square Error (RMSE) between simulated and experimental breakthrough curves.

---

## Numerical Implementation

The transport model is implemented using an explicit finite difference scheme.

Each time step computes:

- advection
- hydrodynamic dispersion
- attachment
- detachment
- blocking
- straining

The outlet concentration is recorded to generate the breakthrough curve.

Repeated model evaluations required during optimization were accelerated using **Numba**, while **SciPy's Differential Evolution** algorithm was used for simultaneous parameter estimation.

---

## Libraries Used

- **NumPy** – numerical computations and array operations
- **Pandas** – experimental data processing
- **Matplotlib** – visualization of breakthrough curves and retention profiles
- **SciPy** – Differential Evolution optimization
- **Numba** – JIT compilation for faster repeated simulations

---

## Results

The final model successfully reproduces the experimental breakthrough curve by combining multiple transport mechanisms within a single numerical framework.

Replacing manual parameter selection with Differential Evolution automated the calibration process, allowing all model parameters to be estimated simultaneously while minimizing RMSE. This significantly reduced the need for repeated manual simulations and provided a reproducible parameter estimation workflow.

---

## Skills Demonstrated

This project involved the implementation of:

- Numerical solution of partial differential equations using finite difference methods
- Scientific computing using Python
- Mathematical modelling of physical systems
- Inverse parameter estimation
- Global optimization using Differential Evolution
- Performance optimization using Numba
- Experimental data processing and model validation

---

## Future Improvements

Possible extensions include:

- simultaneous calibration using multiple experimental datasets,
- uncertainty and sensitivity analysis of optimized parameters,
- incorporation of additional environmental variables such as pH, temperature and ionic strength,
- prediction of transport parameters directly from experimentally measurable properties,
- extension to multi-particle or multi-species transport models.
