# Results Overview

## Model Performance Comparison

| Model | RMSE | R² Score | Characteristics |
|-------|------|----------|-----------------|
| **PIML (This Study)** | **0.2532** | **0.9353** | Physically interpretable, outputs activation energy $E_a$ |
| Standard DNN | 0.2518 | 0.9360 | Purely data-driven, black-box model |
| Random Forest | 0.7222 | 0.4740 | Conventional ensemble learning |
| XGBoost | 0.7179 | 0.4803 | Conventional ensemble learning |

## AI-Discovered Optimal Material Composition

| Parameter | Value |
|-----------|-------|
| **Material System** | ZrO₂ - Sc - Mg co-doped |
| **Sc Doping Concentration** | 7.50 mol% |
| **Mg Doping Concentration** | 3.19 mol% |
| **Total Dopant Content** | 10.68% |
| **Predicted Conductivity @800°C** | 0.092 S/cm |
| **Recommended Sintering Temperature** | 1505°C |
| **Stability Assessment** | Metastable (tetragonal/cubic mixed phase) |

## Key Result Figures

### PIML Model Prediction Performance

![PIML Predicted vs Actual Values and Activation Energy Distribution](../assets/images/piml_prediction_and_ea_dist.png)
*PIML model prediction performance on the validation set (left) and predicted activation energy distribution (right). R² = 0.9353, with activation energies concentrated around ~1 eV, consistent with physical expectations.*

### Material Chemistry Latent Space

![t-SNE Latent Space Visualization](../assets/images/paper_latent_space.png)
*t-SNE dimensionality-reduced material chemistry latent space. Different colors represent different primary dopant elements; the model spontaneously learned chemical clustering trends.*

### Feature Importance Analysis

![Activation Energy Feature Importance](../assets/images/paper_feature_importance_Ea.png)
*Feature permutation importance analysis for activation energy $E_a$ prediction. Sintering duration and dopant count are the most critical influencing factors.*

### Inverse Design Optimization Process

![Genetic Algorithm Optimization Curve](../assets/images/paper_inverse_design_ga.png)
*Genetic algorithm-driven ternary co-doping composition optimization process, converging to the optimal region within approximately 5 generations.*

### Lattice Strain Theory Verification

![Activation Energy vs Dopant Radius Relationship](../assets/images/paper_strain_theory_verification.png)
*Relationship between activation energy and average dopant ionic radius, validating the physical trend predicted by lattice strain theory.*

### Active Learning Efficiency Comparison

![AI-Guided vs Random Strategy](../assets/images/paper_active_learning.png)
*The AI-guided strategy discovered a near-optimal material in only 1 iteration, whereas the random strategy failed to achieve comparable performance after 15 iterations.*

### Uncertainty Quantification Calibration

![UQ Calibration Results](../assets/images/paper_uq_calibration.png)
*Monte Carlo Dropout uncertainty estimation; the majority of true values fall within the 95% confidence interval.*

### Stability Phase Diagram

![Phase Stability Mapping](../assets/images/validation_stability_map.png)
*Position of the AI-discovered material (gold pentagram) in the phase stability diagram, located in the metastable region with high conductivity potential.*

### Molecular Dynamics Validation

![PIML vs MD Computational Comparison](../assets/images/paper_computational_validation.png)
*Comparison between PIML predictions and CHGNet molecular dynamics simulations; ranking of all 4 samples is 100% consistent.*

### DFT Formation Energy Analysis

![DFT Formation Energy](../assets/images/paper_dft_formation_energy.png)
*DFT formation energy comparison: the AI-recommended material exhibits negative formation energy (stable), while the high-concentration Mg-doped variant exhibits positive formation energy (unstable).*
