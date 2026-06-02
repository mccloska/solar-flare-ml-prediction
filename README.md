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
- [Data & Methodology](#data--methodology)
- [Models & Algorithms](#models--algorithms)
- [Results & Evaluation](#results--evaluation)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)
- [References](#references)

---

## Overview

This repository contains machine learning implementations for predicting solar flares based on sunspot characteristics. The project builds upon traditional McIntosh classification-based forecasting methods and explores modern ML approaches to enhance operational flare forecast services.

**Primary Goal**: Develop and evaluate ML-based solar flare prediction models to enhance operational flare forecast services.

---

## Project Description

### Background

Historically, McIntosh classifications of sunspots have been utilized for the prediction of solar flares. Modern operational flare forecast services still rely upon these classifications for their operational forecasts.

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
│   ├── data/                     # Data storage directory (may contain raw/processed data)
│   ├── plots/                    # Generated plots and visualizations
│   └── [outputs]/                # ROC curves, metric comparisons, feature importance plots
│
└── Development Files
    ├── .vscode/                  # VSCode configuration
    └── __pycache__/              # Python cache directory (auto-generated)
```

### Script Descriptions

#### Machine Learning Pipeline
- **`machine_learn_kfold.py`** (Main): Implements K-Fold stratified cross-validation across solar cycles. Evaluates multiple algorithms (LR, LDA, KNN, CART, RFC) with custom skill score metrics (BSS, TSS).
- **`machine_learn_full.py`** (Alternative): Trains on complete Solar Cycle 22, tests on Solar Cycle 23. Includes feature importance comparisons and calibration analysis.

#### Data Processing
- **`processing.py`**: Processes raw NOAA SWPC SRS (Solar Region Summary) and Event files, linking AR properties with X-ray flare occurrences.
- **`get_data.py`**: Downloads solar data directly from NOAA FTP server for specified years.
- **`swpc_proc.py`**: Utility functions for reading and parsing SWPC data formats.

#### Evaluation & Visualization
- **`calibration_curve_plot.py`**: Generates reliability diagrams for model probability calibration.
- **`ss_custom.py`**: Custom skill score calculations (Brier Skill Score, True Skill Statistic).
- **`rfc_importance.py`**: Analyzes and visualizes feature importance from Random Forest models.

#### Data Files
- **`mcint_ml22.csv`**: McIntosh classification data + flare labels for Solar Cycle 22
- **`mcint_ml23.csv`**: McIntosh classification data + flare labels for Solar Cycle 23
- **`mcint_ml.csv`**: Additional McIntosh dataset

---

## Getting Started

### Prerequisites

- Python 3.7+
- pip or conda package manager
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
   (Note: If `requirements.txt` doesn't exist, you can install dependencies manually from the imports in the scripts)

---

## Usage

### Running the ML Pipeline

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

### Data Retrieval

To download solar data from NOAA:
```bash
python get_data.py
```
This will download SRS and Event files to the `data/` directory.

### Data Processing

To process raw NOAA SWPC data files:
```bash
python processing.py
```
(Note: Requires NOAA raw SRS and Event files in appropriate subdirectories)

---

## Data & Methodology

### Data Sources

- **Solar cycles**: Data from multiple independent solar cycle periods (Cycles 22 & 23)
- **McIntosh classifications**: Sunspot classification attributes with evolution codes
- **Flare labels**: Historical solar flare occurrence within 24-hour windows

### Feature Engineering

Features are derived from McIntosh classification components:
- **Zurich classification** (sunspot area, height, complexity)
- **Penumbral class** (magnetic field configuration)
- **Reduced class** (sunspot compactness)
- **McIntosh evolution codes** (static and dynamic properties)

### Cross-Validation Strategy

- **Solar cycle-based splitting**: Models trained on Cycle 22, tested on Cycle 23 (or vice versa)
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
- **Support Vector Machines (SVM)**: Non-linear classification (in full pipeline)

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

Each script includes:
- **Docstrings**: Function documentation (where present)
- **Comments**: Explanations of complex logic, especially around feature encoding

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

### Recommended Reading

- Space Weather prediction literature
- Solar flare prediction studies
- Machine learning classification techniques
- Cross-validation methodologies for time-series data

---

## Contact & Support

For questions, issues, or suggestions regarding this project:

- **Author**: Aoife McCloskey
- **Email**: mccloska@tcd.ie
- **Repository**: https://github.com/mccloska/solar-flare-ml-prediction

---

**Last Updated**: June 2026  
**Status**: Active Research Project
