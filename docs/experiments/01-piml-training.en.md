# Physics-Informed Neural Network (PIML) Material Conductivity Prediction Experiment Report

## 1. Experimental Background and Objectives
This experiment aims to predict the electrical conductivity of materials using machine learning methods while simultaneously inferring physically meaningful parameters (such as the activation energy $E_a$). The experiment employs a **Physics-Informed Neural Network (PIML)** architecture that embeds the Arrhenius physical law as a constraint layer within the deep learning model, thereby improving the model's generalization capability and interpretability.

## 2. Experimental Setup and Methods

### 2.1 Dataset
* **Data Source**: Extracted from a local DuckDB database via the `MaterialDataProcessor`.
* **Data Scale**: A total of **1351** samples were loaded; the ETL output DataFrame shape was **(1351, 14)** (including non-feature columns such as the target column `log_conductivity` and the temperature column `temperature_kelvin`).
* **Feature Engineering**:
    * **Numerical Features**: Including total dopant fraction, average ionic radius, average valence, number of dopants, maximum sintering temperature, and total sintering duration.
    * **Categorical Features**: Synthesis method, primary dopant element.
    * **Text Features**: Material source and purity (processed using TF-IDF and SVD dimensionality reduction).
* **Model Input Dimensionality**: The features input to the network consist of "6 numerical features + One-Hot encoded expansions of 2 categorical features + SVD-reduced text features (16 dimensions)". Therefore, the final dimensionality depends on the actual number of One-Hot categories (denoted as `X_train.shape[1]` in the script) and does not equal the 14 columns of the DataFrame.
* **Data Split**: The training-to-validation set ratio was 8:2, with a random seed of 42.

### 2.2 Model Architecture
A custom `PhysicsInformedNet` was adopted, consisting of two components:
1.  **Data-Driven Encoder**: A multi-layer perceptron (MLP) that extracts latent information from input features and predicts two physical parameters:
    * **Activation Energy ($E_a$)**: Ensured to be positive via the Softplus activation function.
    * **Pre-exponential Factor ($\log A$)**.
2.  **Physics Constraint Layer**: Enforces the model to follow the Arrhenius equation for computing the final conductivity prediction $\log(\sigma)$:
    $$
    \log_{10}(\sigma) = \log_{10}(A) - \log_{10}(T) - \frac{E_a}{k_B \cdot T \cdot \ln(10)}
    $$
    where $k_B$ is the Boltzmann constant and $T$ is the absolute temperature.

### 2.3 Training Parameters
* **Optimizer**: AdamW (Learning Rate = 1e-3, Weight Decay = 1e-4).
* **Loss Function**: Mean Squared Error Loss (MSELoss).
* **Epochs**: 300 Epochs.
* **Batch Size**: 32.

## 3. Training Process Analysis

Based on the training log (`1.log`):
* **Convergence Behavior**: The model converged rapidly during training. The initial validation loss was **3.0193**, which dropped sharply to **0.4678** by Epoch 10.
* **Stabilization Phase**: After approximately Epoch 60, the validation loss converged to fluctuations within the **0.06 - 0.13** range, with an overall stable trend.
* **Best Model**: A near-optimal value was reached around Epoch 250 (Loss $\approx$ 0.0659), after which the model fluctuated between 0.065 and 0.085. Based on the validation loss trajectory, no significant rebound was observed (the script did not record the training loss curve, so a rigorous overfitting assessment cannot be made).

## 4. Results Analysis

### 4.1 Quantitative Evaluation
* **Final Performance Metrics**: The model achieved a root mean square error (**RMSE**) of **0.2532** and a coefficient of determination **$R^2 \approx 0.9353$** on the validation set. Considering that the target variable is conductivity on a $\log_{10}$ scale, an RMSE of 0.2532 corresponds to a typical multiplicative error of approximately $10^{0.2532}\approx 1.79$ (i.e., within approximately a **factor of 2** in most cases), indicating high accuracy.

### 4.2 Visual Analysis
Based on the generated analysis plots:

![PIML Prediction and Ea Distribution](../assets/images/piml_prediction_and_ea_dist.png)

1.  **Prediction vs. Actual**:
    * **Left Panel Analysis**: Data points are tightly distributed around the red dashed line ($y=x$).
    * **Linear Relationship**: The model exhibits strong linear correlation across the plotted value range ($R^2 \approx 0.9353$).
    * **Error Distribution**: A small number of outliers exist in the low-conductivity region (-6 to -7), but the fitting performance is excellent in the high-frequency region (-1 to -4).

2.  **Predicted Activation Energy Distribution (Predicted Activation Energy $E_a$)**:
    * **Right Panel Analysis**: The activation energy $E_a$ inferred by the model exhibits a unimodal distribution, predominantly concentrated at approximately **1 eV** (as shown in the figure).
    * **Physical Plausibility**: This magnitude is consistent with the conduction activation energy range reported for common oxide solid electrolytes (e.g., zirconia-based systems), demonstrating that the PIML model outputs physically meaningful intermediate parameters while fitting conductivity.

## 5. Conclusions
1.  **Model Effectiveness**: The PIML model achieved low prediction error (RMSE 0.2532) with a small dataset (1351 samples), validating the effectiveness of incorporating physical constraints.
2.  **Physical Interpretability**: The model successfully decoupled the influence of temperature on conductivity and produced a physically reasonable distribution of activation energy ($E_a$) parameters. This makes the model more than a mere "black box" — it can also assist researchers in analyzing the physical properties of materials.
3.  **Directions for Improvement**: Although the overall fit is good, there is room for improvement in the very low conductivity region. Future work may explore oversampling of low-conductivity samples or adjusting loss function weights.
