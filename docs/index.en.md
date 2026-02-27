# AI-Driven Optimization of Zirconia Ionic Conductivity

## Project Overview

This project employs **Physics-Informed Machine Learning (PIML)** methods, integrating the Arrhenius physical law with deep learning, to achieve high-accuracy prediction, mechanistic interpretation, and inverse design of novel materials for the ionic conductivity of zirconia (ZrO₂)-based solid electrolytes.

## Documentation Site Scope

- This GitHub Pages site is a static documentation portal for data cleaning workflows, experiment reports, result figures, and equations.
- This site **does not run** Python training scripts, MySQL ETL jobs, or MD/DFT computations. Those tasks must run in local or server environments.
- Source repositories:
  - Data cleaning: <https://github.com/lanhung/material-conductivity-data-clean>
  - ML analysis: <https://github.com/lanhung/material-conductivity-data-analysis-ml>

## Research Highlights

| Metric | Result |
|--------|--------|
| **PIML Model Accuracy** | RMSE = 0.2532, R² = 0.9353 |
| **AI-Discovered Optimal Composition** | ZrO₂ + Sc(7.5%) + Mg(3.2%), predicted conductivity 0.092 S/cm @800°C |
| **Active Learning Efficiency** | Near-optimal material discovered in only 1 iteration, 15× faster than random strategy |
| **Computational Validation** | PIML prediction ranking 100% consistent with molecular dynamics simulations |

## Technical Approach

This study establishes a complete closed-loop pipeline of **"Data Cleaning → Model Training → Mechanistic Interpretation → Inverse Design → Multi-Scale Validation"**:

1. **[Data Cleaning](data-cleaning/index.md)**: A hybrid pipeline combining Python, LLM, and SQL to standardize 2,010 raw literature records into 1,351 high-quality samples
2. **[PIML Model Training](experiments/01-piml-training.md)**: Embedding the Arrhenius equation into neural networks for physics-constrained conductivity prediction
3. **[In-Depth Mechanistic Interpretation](experiments/02-mechanism-analysis.md)**: Latent space visualization, feature importance analysis, and cross-element generalization testing
4. **[Baseline Model Comparison](experiments/03-baseline-benchmark.md)**: PIML vs DNN vs Random Forest vs XGBoost
5. **[Inverse Materials Design](experiments/04-inverse-design.md)**: Genetic algorithm-driven search for optimal co-doping compositions
6. **[Active Learning](experiments/05-active-learning.md)**: Uncertainty quantification and AI-guided efficient material discovery strategy
7. **[Stability Screening](experiments/06-stability-screening.md)**: Thermodynamic stability prediction based on Shannon ionic radii
8. **[Molecular Dynamics Validation](experiments/07-md-validation.md)**: Validation via CHGNet machine learning force field MD simulations
9. **[DFT Computational Verification](experiments/08-dft-verification.md)**: First-principles computational framework using Quantum Espresso

## Core Model Architecture

The PIML model comprises two components:

- **Data-Driven Encoder**: A multilayer perceptron that extracts latent information from material features
- **Physics-Constrained Layer**: Enforces adherence to the Arrhenius equation $\log_{10}(\sigma) = \log_{10}(A) - \log_{10}(T) - \frac{E_a}{k_B \cdot T \cdot \ln(10)}$

This enables the model to maintain high predictive accuracy while outputting physically meaningful activation energy ($E_a$) parameters.

## Dataset

- **Sample Size**: 1,351 zirconia conductivity measurement records
- **Source**: Literature data mining
- **Dopant Elements**: Y, Sc, Yb, Gd, Mg, etc.
- **Temperature Range**: 600–1000°C
- **Conductivity Range**: 10⁻⁶ ~ 10⁻¹ S/cm
