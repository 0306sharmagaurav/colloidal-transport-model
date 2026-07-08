# Colloidal Transport Modelling in Saturated Porous Media

## Project Overview

This project models the transport of microplastic particles through a saturated sand column using a one-dimensional advection-dispersion transport model. The objective is to reproduce experimentally observed breakthrough curves (BTCs) by incorporating the major particle retention mechanisms and estimating their governing parameters through inverse modelling.

The model was developed incrementally. Starting with conservative tracer transport, additional physical mechanisms such as attachment, detachment, blocking and straining were introduced one at a time to understand their individual influence on particle transport. The final stage replaces manual parameter tuning with Differential Evolution optimization to estimate the parameter set that minimizes the difference between simulated and experimental BTCs.

The work was carried out as part of a summer research project on microplastic transport in porous media.

---

## Problem Statement

The movement of colloidal particles in porous media is controlled by several interacting physical processes. While conservative tracers mainly undergo advection and dispersion, microplastic particles additionally experience retention mechanisms that alter their transport behaviour.

The aim of this project is to:

- simulate particle transport through a laboratory soil column,
- incorporate the dominant retention mechanisms,
- compare simulated and experimental breakthrough curves, and
- estimate physically meaningful model parameters using optimization instead of manual trial-and-error.

---

## Methodology

The transport model is based on the one-dimensional Advection-Dispersion Equation (ADE).

The project was developed in the following sequence:

1. **Tracer Transport**
   - Simulated conservative tracer transport considering only advection and dispersion.
   - Used tracer experiments to understand pore velocity, dispersion and breakthrough behaviour.

2. **Particle Attachment**
   - Introduced first-order attachment to represent particle deposition on collector surfaces.
   - Attachment coefficient was related to attachment efficiency (α) through filtration theory.

3. **Particle Detachment**
   - Added reversible release of previously retained particles.
   - Studied its influence on BTC peak concentration and tailing.

4. **Blocking**
   - Implemented Langmuir-type blocking using a finite attachment capacity (`Smax`).
   - Investigated how progressive occupation of attachment sites affects transport.

5. **Straining**
   - Included particle straining as an additional retention mechanism.
   - Extended the model to allow depth-dependent straining through an exponentially varying straining coefficient.

6. **Inverse Parameter Estimation**
   - Replaced manual parameter tuning with Differential Evolution optimization.
   - Simultaneously estimated:
     - attachment efficiency (α)
     - detachment coefficient (`kdet`)
     - straining coefficient (`kstr0`)
     - depth dependency coefficient (`β`)
     - maximum retention capacity (`Smax`)
   - Model performance was evaluated using Root Mean Square Error (RMSE) between simulated and experimental BTCs.

---

## Numerical Implementation

The model is implemented using an explicit finite difference scheme.

For each time step, the code computes:

- advection
- hydrodynamic dispersion
- attachment
- detachment
- blocking
- straining

The outlet concentration is recorded to generate the simulated breakthrough curve.

The optimized parameter set is obtained using `scipy.optimize.differential_evolution`, while `Numba` is used to accelerate repeated model evaluations during optimization.

---

## Repository Structure

```
.
├── notebooks/          # Development notebooks and simulations
├── data/               # Experimental BTC data
├── figures/            # Generated plots (if included)
├── README.md
└── requirements.txt
```

*(Modify the folder names above if your repository structure is different.)*

---

## Installation

Clone the repository

```bash
git clone https://github.com/<username>/<repository>.git
cd <repository>
```

Install the required libraries

```bash
pip install -r requirements.txt
```

or install manually

```bash
pip install numpy pandas matplotlib scipy numba openpyxl
```

---

## Usage

1. Place the experimental Excel file inside the data folder.
2. Update the file path in the notebook if necessary.
3. Run the notebook sequentially.

The notebook contains two main workflows:

- Forward simulation using user-defined parameters.
- Parameter estimation using Differential Evolution.

The optimization returns the parameter set that minimizes the RMSE between simulated and experimental breakthrough curves.

---

## Results

The final model is capable of reproducing the experimental breakthrough curve by considering:

- attachment,
- detachment,
- blocking,
- depth-dependent straining.

Replacing manual parameter tuning with Differential Evolution made it possible to estimate all fitting parameters simultaneously, removing the need for repeated trial-and-error simulations.

---

## Libraries Used

- **NumPy** — numerical computations
- **Pandas** — experimental data processing
- **Matplotlib** — plotting breakthrough curves and retention profiles
- **SciPy** — Differential Evolution optimization
- **Numba** — acceleration of repeated model evaluations

---

## Future Improvements

Some possible extensions include:

- simultaneous calibration using multiple experimental datasets,
- inclusion of additional environmental factors such as temperature and solution chemistry,
- uncertainty and sensitivity analysis of optimized parameters,
- validation against independent experiments,
- extension to multi-species or multi-particle transport.

---

## References

The modelling approach is based on concepts from colloid filtration theory and particle transport in saturated porous media, including advection-dispersion transport, attachment-detachment kinetics, blocking and straining mechanisms.
