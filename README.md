# Machine Learning - Sunspot Characteristics & Flare Forecasting

**Author**: Aoife McCloskey  
**Email**: mccloska@tcd.ie

---

## 📋 Table of Contents

- [Overview](#overview)
- [Project Description](#project-description)
- [Key Features](#key-features)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
  - [Jupyter Notebooks](#jupyter-notebooks)
  - [Python Scripts](#python-scripts)
- [Data & Methodology](#data--methodology)
- [Models & Algorithms](#models--algorithms)
- [Results & Evaluation](#results--evaluation)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)
- [References](#references)

---

## Overview

This repository contains machine learning implementations for predicting solar flares based on sunspot characteristics. The project builds upon traditional McIntosh classification-based forecasting and includes both interactive Jupyter notebooks and production Python scripts.

**Primary Goal**: Develop and evaluate ML-based solar flare prediction models to enhance operational flare forecast services.

---

## Project Description

### Background

Historically, McIntosh classifications of sunspots have been utilized for the prediction of solar flares. Modern operational flare forecast services still rely upon these classifications for their predictions.

### Objectives

1. **Build ML Models**: Construct a set of machine learning models to predict solar flares within a 24-hour period
2. **Compare Performance**: Evaluate ML approaches against traditional Poisson-based forecasting models
3. **Validate Results**: Train and test algorithms using data from multiple independent solar cycle periods
4. **Feature Analysis**: Explore the importance of individual McIntosh components on model performance
5. **Address Solar Cycle Dependency**: Investigate and mitigate solar cycle dependencies in predictions

### Key Contributions

- Application of multiple ML techniques (algorithms compared across comprehensive metrics)
- Cross-validation across multiple solar cycles to ensure robustness
- Skill score calculations for direct comparison with Poisson-based forecasts
- Feature importance analysis with physical interpretation
- Investigation of solar cycle effects on model generalization

---

## Key Features

✅ Multiple Machine Learning Algorithms  
✅ Cross-Solar-Cycle Validation  
✅ Comprehensive Performance Metrics (Skill Scores, BSS, TSS, ROC-AUC)  
✅ Feature Importance Analysis  
✅ Solar Cycle Dependency Analysis  
✅ McIntosh Classification-based Features  
✅ 24-hour Flare Prediction Window  
✅ Interactive Jupyter Notebooks  
✅ Calibration Analysis & Reliability Diagrams  

---

## Project Structure

```
solar-flare-ml-prediction/
├── README.md                      # Project documentation (this file)
├── Home.md                        # Wiki home page
├── References.md                  # Literature references
│
├── Data Files (Root Level)
│   ├── mcint_ml22.csv            # McIntosh data for Solar Cycle 22 (training set)
│   ├── mcint_ml23.csv            # McIntosh data for Solar Cycle 23 (test set)
│   └── mcint_ml.csv              # Additional McIntosh data
│
├── notebooks/                     # Jupyter notebooks for interactive analysis
│   ├── 01_Data_Overview_and_Exploration.ipynb           # Data exploration & visualization
│   ├── 02_ML_Pipeline_and_Evaluation.ipynb              # K-Fold ML pipeline with 5 algorithms
│   ├── 03_Feature_Importance_Analysis.ipynb             # Feature importance breakdown
│   └── 04_Cycle_to_Cycle_Transfer_Learning.ipynb        # Cycle 22 → Cycle 23 cross-validation
│
├── Core ML Scripts
│   ├── machine_learn_kfold.py    # K-Fold cross-validation ML pipeline
│   ├── machine_learn_full.py     # Full cycle-to-cycle ML training
│   ├── calibration_curve_plot.py # Calibration curve visualization & reliability diagrams
│   │
│   ├── Feature Engineering & Processing
│   ├── processing.py             # NOAA SWPC SRS & Event data processing
│   ├── mci_classification_ml.py  # McIntosh classification utilities
│   │
│   ├── Evaluation & Analysis
│   ├── ss_custom.py              # Custom scoring functions (BSS, TSS)
│   ├── rfc_importance.py         # Random Forest feature importance analysis
│   │
│   ├── Data Retrieval
│   ├── get_data.py               # FTP data retrieval from NOAA SWPC server
│   ├── swpc_proc.py              # SWPC data processing utilities
│   └── realtime_forecast_mcint.py # Real-time forecasting module
│
├── Output Directories
│   ├── data/                     # Data storage directory
│   ├── plots/                    # Generated plots and visualizations
│   └── [outputs]/                # ROC curves, metric comparisons, feature importance plots
│
└── Development Files
    ├── .vscode/                  # VSCode configuration
    └── __pycache__/              # Python cache directory (auto-generated)
```

---

## Getting Started

### Prerequisites

- Python 3.8+
- pip or conda package manager
- Jupyter Notebook (for interactive notebooks)
- Basic familiarity with machine learning and solar physics concepts

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/mccloska/solar-flare-ml-prediction.git
   cd solar-flare-ml-prediction
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
   Or install manually:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn scipy jupyter
   ```

---

## Usage

### Jupyter Notebooks

The easiest way to explore this project is through the interactive Jupyter notebooks:

```bash
jupyter notebook
```

Then navigate to the `notebooks/` directory and open them in order:

| Notebook | Purpose |
|----------|---------|
| **01_Data_Overview_and_Exploration.ipynb** | Load data, explore distributions, visualize McIntosh features |
| **02_ML_Pipeline_and_Evaluation.ipynb** | K-Fold cross-validation with 5 ML algorithms (LR, LDA, KNN, CART, RFC) |
| **03_Feature_Importance_Analysis.ipynb** | Analyze which McIntosh components matter most for predictions |
| **04_Cycle_to_Cycle_Transfer_Learning.ipynb** | Train on Cycle 22, test on Cycle 23 - evaluate cross-cycle generalization |

Each notebook includes visualizations, performance metrics, and detailed explanations.

### Python Scripts

#### Option 1: K-Fold Cross-Validation (Recommended)
```bash
python machine_learn_kfold.py
```
When prompted:
- **Which cycle to train and test on?** → Enter `22` or `23`
- **Which method would you like to use?** → Options: `static`, `evol`, `both`, `sep_zpc`, `zpc1`, `zpc1_sep`, `zpc2_sep`, `zpc2`, `zpc_both`, `one_hot_sep`
- **Would you like to encode?** → Enter `yes` or `no`

Output: ROC curves, BSS/TSS comparison plots, feature importance boxplots

#### Option 2: Full Cycle-to-Cycle Training
```bash
python machine_learn_full.py
```
When prompted:
- **Which method would you like to use?** → Same options as above

Output: Calibration diagrams, ROC curves, comparative feature importance plots

#### Data Retrieval
```bash
python get_data.py
```
Downloads SRS and Event files to the `data/` directory from NOAA SWPC server.

#### Data Processing
```bash
python processing.py
```
Processes raw NOAA SWPC data files. (Requires NOAA raw SRS and Event files)

---

## Data & Methodology

### Data Sources

- **Solar cycles**: Data from independent solar cycle periods (Cycles 22 & 23)
- **McIntosh classifications**: Sunspot classification attributes with evolution codes
- **Flare labels**: Historical solar flare occurrence within 24-hour windows

### Feature Engineering

Features are derived from McIntosh classification components:
- **Zurich classification** (sunspot area, height, complexity)
- **Penetration class** (magnetic field configuration)
- **Reduced class** (sunspot compactness)
- **McIntosh evolution codes** (static and dynamic properties)

### Cross-Validation Strategy

- **Solar cycle-based splitting**: Models trained on Cycle 22, tested on Cycle 23
- **K-Fold stratified sampling**: 10-fold stratification respects temporal and class dependencies
- **Time-series considerations**: Respects temporal dependencies in solar data

---

## Models & Algorithms

The project evaluates and compares multiple machine learning algorithms:

- **Logistic Regression (LR)**: Baseline linear classifier
- **Linear Discriminant Analysis (LDA)**: Linear classification with dimensionality reduction
- **K-Nearest Neighbors (KNN)**: Non-parametric instance-based learning
- **Decision Tree / CART**: Single tree classifier with feature importance
- **Random Forest Classifier (RFC)**: Ensemble method with robust feature importance
- **Support Vector Machines (SVM)**: Non-linear classification (in notebooks)

Each model is evaluated against:
- **Poisson-based baseline forecasts** (operational standard)
- **Multiple performance metrics** (BSS, TSS, ROC-AUC, Accuracy, Precision, Recall)
- **Cross-cycle generalization** capability

---

## Results & Evaluation

### Metrics

- **Brier Skill Score (BSS)**: Probabilistic skill score comparing to Poisson baseline
- **True Skill Statistic (TSS)**: Binary classification skill metric
- **Accuracy, Precision, Recall**: Standard classification metrics
- **ROC-AUC**: Area under the receiver operating characteristic curve
- **F1-Score**: Balanced classification performance metric
- **Confusion Matrices**: Detailed error analysis with true/false positives and negatives
- **Calibration Analysis**: Reliability diagrams for probability calibration assessment

### Output Files

The scripts generate:
- **ROC curves**: `ROC_curve_*.eps` (one per algorithm per cross-validation run)
- **Skill score comparisons**: `algorithm_comp_bss_*.eps`, `algorithm_comp_tss_*.eps`
- **Feature importance**: `feat_importances_*.eps` (boxplots and bar charts)
- **Calibration diagrams**: `*_reliability_diagram_*.png`
- **Pickled feature data**: `kfold_feature_importance.data`

---

## Documentation

### Code Documentation

Each script and notebook includes:
- **Docstrings**: Function documentation (where present)
- **Comments**: Explanations of complex logic, especially around feature encoding
- **Markdown cells**: Detailed explanations in notebooks

### Customization

Key parameters can be modified directly in scripts:
- **Data file paths**: `filename_train`, `filename_test` in ML scripts
- **Cross-validation folds**: `n_splits` parameter in `StratifiedKFold()`
- **Feature selection**: Adjust column indices `a:b` for different feature combinations
- **Algorithm choices**: Comment/uncomment models in `models` list
- **Visualization colors**: Modify `colors` array for plot aesthetics

---

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes with clear messages
4. Push to your branch
5. Open a Pull Request with a description of changes

### Guidelines

- Follow PEP 8 code style
- Add docstrings to new functions
- Include comments for complex logic
- Test with different data and parameter combinations
- Update README if adding new functionality or scripts

---

## License

This project is provided as-is for research and educational purposes. Please cite appropriately if used in academic work.

---

## References

### Key Publications & Concepts

- **McIntosh Classification System**: Standard for sunspot characterization
- **Poisson-based Flare Forecasting**: Traditional operational approach
- **Solar Cycle Effects**: Understanding cycle-dependent solar activity patterns
- **Machine Learning in Solar Physics**: Emerging applications of ML to space weather prediction

See `References.md` for a comprehensive list of literature references and key citations.

---

## Contact & Support

For questions, issues, or suggestions regarding this project:

- **Author**: Aoife McCloskey
- **Email**: mccloska@tcd.ie
- **Repository**: https://github.com/mccloska/solar-flare-ml-prediction

---

**Last Updated**: June 2026  
**Status**: Active Research Project
