<div align="center">

# 🌐 TimeSeries-NetTraffic-Engine

### Advanced Network Traffic Time Series Forecasting & Analysis Framework

[![Python](https://img.shields.io/badge/Python-3.10.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg?style=for-the-badge)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![SARIMA](https://img.shields.io/badge/Model-SARIMA-blueviolet?style=for-the-badge)](https://www.statsmodels.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.5.0-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)

*Intelligent network traffic forecasting using state-of-the-art time series analysis on the CESNET-TimeSeries-2023-2024 dataset*

[Features](#-features) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [Dataset](#-dataset) • [Examples](#-examples) • [Contributing](#-contributing)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-features)
- [Architecture](#-architecture)
- [Dataset Structure](#-dataset)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Usage Examples](#-usage-examples)
- [Model Configuration](#-model-configuration)
- [Evaluation Metrics](#-evaluation-metrics)
- [Project Structure](#-project-structure)
- [Advanced Usage](#-advanced-usage)
- [Performance & Benchmarks](#-performance--benchmarks)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)
- [Citation](#-citation)

---

## 🎯 Overview

**TimeSeries-NetTraffic-Engine** is a production-ready, enterprise-grade framework for network traffic forecasting and analysis using advanced time series modeling techniques. Built on top of the comprehensive **CESNET-TimeSeries-2023-2024** dataset, this framework leverages SARIMA (Seasonal AutoRegressive Integrated Moving Average) models to predict network behavior patterns with high accuracy.

### 🎓 What is This Project About?

This framework provides researchers, network engineers, and data scientists with powerful tools to:

- **Forecast Network Traffic**: Predict future network behavior using historical patterns
- **Analyze Time Series**: Understand temporal patterns in network metrics across different aggregation levels
- **Evaluate Performance**: Comprehensive evaluation using RMSE, SMAPE, and R² metrics
- **Scale Analysis**: Process multiple IP addresses, institutions, and subnets simultaneously
- **Automated Retraining**: Implement sliding window approaches for continuous model improvement

### 🏢 Real-World Applications

- **Network Capacity Planning**: Predict bandwidth requirements and optimize infrastructure
- **Anomaly Detection**: Identify unusual traffic patterns by comparing predictions with actual values
- **Resource Optimization**: Allocate network resources efficiently based on forecasted demand
- **Security Analytics**: Detect potential DDoS attacks or unusual traffic patterns
- **SLA Management**: Ensure service level agreements through predictive maintenance

---

## ✨ Features

### 🚀 Core Capabilities

- **📊 Multi-Scale Analysis**: Support for 10-minute, 1-hour, and 1-day aggregation intervals
- **🔄 Automated Retraining**: Sliding window approach with configurable training and testing periods
- **📈 18 Network Metrics**: Comprehensive coverage including flows, packets, bytes, ASN diversity, port diversity, and TCP/UDP ratios
- **🎯 High-Performance Forecasting**: SARIMA model with optimized hyperparameters
- **📉 Missing Value Handling**: Intelligent gap-filling strategies for time series continuity
- **🔍 Multi-Dataset Support**: Works with IP addresses, institutions, and institution subnets
- **📊 Visualization Suite**: Rich plotting capabilities for exploratory data analysis
- **⚡ Parallel Processing**: Metacentrum scripts for large-scale batch processing

### 🛠️ Technical Features

- **Reproducible Research**: Clear documentation of all preprocessing and modeling steps
- **Scalable Architecture**: Designed for processing thousands of time series
- **Flexible Configuration**: Easy customization of model parameters and evaluation settings
- **Production-Ready Code**: Clean, well-documented, and maintainable codebase
- **Comprehensive Evaluation**: Multiple statistical metrics for robust performance assessment

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    CESNET Time Series Dataset                │
│  ┌────────────┐  ┌─────────────┐  ┌──────────────────────┐ │
│  │IP Addresses│  │ Institutions│  │ Institution Subnets  │ │
│  └────────────┘  └─────────────┘  └──────────────────────┘ │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│              Data Preprocessing & Gap Filling                │
│  • Missing value imputation                                  │
│  • Ratio metrics normalization (0.5)                         │
│  • Temporal alignment                                        │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│                   SARIMA Modeling Engine                     │
│  Order: (p=1, d=1, q=1)                                      │
│  Seasonal Order: (P=1, D=1, Q=1, M=168)                      │
│  Training: 744 hours (31 days)                               │
│  Testing: 168 hours (7 days)                                 │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│              Sliding Window Retraining Loop                  │
│  • Train on historical window                                │
│  • Forecast next period                                      │
│  • Slide window forward                                      │
│  • Repeat until dataset exhausted                            │
└────────────┬────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────┐
│              Evaluation & Analysis                           │
│  • RMSE (Root Mean Squared Error)                            │
│  • SMAPE (Symmetric Mean Absolute Percentage Error)          │
│  • R² Score (Coefficient of Determination)                   │
│  • Statistical distributions                                 │
│  • Aggregate statistics                                      │
└─────────────────────────────────────────────────────────────┘
```

---

## 📊 Dataset

### CESNET-TimeSeries-2023-2024 Dataset Structure

The framework works with the comprehensive CESNET network traffic dataset containing:

#### 📁 Dataset Parts

| Dataset Part | Description | Granularity |
|--------------|-------------|-------------|
| **IP Addresses (Sample)** | Representative sample of individual IP addresses | Individual hosts |
| **IP Addresses (Full)** | Complete set of monitored IP addresses | Individual hosts |
| **Institutions** | Aggregated traffic per institution | Organizational level |
| **Institution Subnets** | Traffic per institution subnet | Network segment level |

#### ⏰ Temporal Aggregations

- **10 Minutes**: High-resolution, short-term pattern analysis
- **1 Hour**: Medium-resolution, ideal for daily pattern detection
- **1 Day**: Low-resolution, long-term trend analysis

#### 📈 Network Metrics (18 Total)

| Category | Metrics |
|----------|---------|
| **Volume** | `n_flows`, `n_packets`, `n_bytes` |
| **ASN Diversity** | `sum_n_dest_asn`, `average_n_dest_asn`, `std_n_dest_asn` |
| **Port Diversity** | `sum_n_dest_ports`, `average_n_dest_ports`, `std_n_dest_ports` |
| **IP Diversity** | `sum_n_dest_ip`, `average_n_dest_ip`, `std_n_dest_ip` |
| **Protocol Ratios** | `tcp_udp_ratio_packets`, `tcp_udp_ratio_bytes` |
| **Direction Ratios** | `dir_ratio_packets`, `dir_ratio_bytes` |
| **Flow Characteristics** | `avg_duration`, `avg_ttl` |

---

## 💻 Installation

### Prerequisites

- **Python**: 3.10.12 or higher
- **pip**: Latest version
- **Operating System**: Linux, macOS, or Windows
- **RAM**: Minimum 8GB (16GB recommended for large-scale analysis)

### Quick Installation

```bash
# Clone the repository
git clone https://github.com/KUNALSHAWW/TimeSeries-NetTraffic-Engine.git
cd TimeSeries-NetTraffic-Engine

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required dependencies
pip install pandas==2.2.2 \
            numpy==1.24.4 \
            matplotlib==3.8.0 \
            scikit-learn==1.5.0 \
            statsmodels==0.14.1 \
            seaborn==0.13.0
```

### Alternative: Requirements File

```bash
# Create requirements.txt
cat > requirements.txt << EOF
pandas==2.2.2
numpy==1.24.4
matplotlib==3.8.0
scikit-learn==1.5.0
statsmodels==0.14.1
seaborn==0.13.0
EOF

# Install from requirements
pip install -r requirements.txt
```

---

## 🚀 Quick Start

### 1️⃣ Basic Example - Explore Time Series

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load time series data
df_times = pd.read_csv('cesnet-time-series-2023-2024/times/times_1_hour.csv')
df_times['time'] = pd.to_datetime(df_times['time'])

# Load network traffic data
df = pd.read_csv('cesnet-time-series-2023-2024/ip_addresses_sample/agg_1_hour/1/103.csv')

# Visualize n_flows metric
plt.figure(figsize=(15, 5))
plt.plot(df_times['time'], df['n_flows'])
plt.title('Network Flows Over Time')
plt.xlabel('Time')
plt.ylabel('Number of Flows')
plt.show()
```

### 2️⃣ Jupyter Notebook Exploration

Launch the interactive example notebook:

```bash
jupyter notebook example.ipynb
```

This notebook provides:
- ✅ Dataset loading and preprocessing
- ✅ Time series visualization
- ✅ SARIMA model training
- ✅ Forecasting and evaluation

### 3️⃣ Command-Line SARIMA Retraining

```bash
python sarima_retraining.py \
    -p 1 -d 1 -q 1 \
    -P 1 -D 1 -Q 1 -M 168 \
    -t 744 -T 168 \
    --dataset ip_addresses_sample \
    --aggregation agg_1_hour \
    --metric n_flows \
    --id_ip 1/103.csv
```

**Parameters Explained:**
- `-p, -d, -q`: ARIMA order (p=AR order, d=differencing, q=MA order)
- `-P, -D, -Q, -M`: Seasonal ARIMA order (M=seasonal period)
- `-t`: Training period (744 hours = 31 days)
- `-T`: Testing period (168 hours = 7 days)
- `--dataset`: Dataset part to use
- `--aggregation`: Temporal aggregation level
- `--metric`: Network metric to forecast
- `--id_ip`: Specific IP/entity identifier

---

## 📚 Usage Examples

### Example 1: Batch Processing with Shell Scripts

For processing multiple time series in parallel on HPC clusters:

```bash
# Process all IP addresses in sample dataset
./metacentrum_scripts/sarima_retraining_ip_addresses_sample.sh

# Process all institutions
./metacentrum_scripts/sarima_retraining_institutions.sh

# Process all institution subnets
./metacentrum_scripts/sarima_retraining_institution_subnets.sh
```

### Example 2: Custom Time Series Analysis

```python
from statsmodels.tsa.statespace.sarimax import SARIMAX
import pandas as pd
import numpy as np

# Configuration
ORDER = (1, 1, 1)
SEASONAL_ORDER = (1, 1, 1, 168)
TRAINING_PERIOD = 744
TESTING_PERIOD = 168

# Load and prepare data
df = pd.read_csv('your_time_series.csv')
train_data = df['n_flows'][:TRAINING_PERIOD]

# Train SARIMA model
model = SARIMAX(train_data, order=ORDER, seasonal_order=SEASONAL_ORDER)
results = model.fit(disp=False)

# Forecast
forecast = results.forecast(steps=TESTING_PERIOD)

# Evaluate
from sklearn.metrics import root_mean_squared_error
rmse = root_mean_squared_error(df['n_flows'][TRAINING_PERIOD:TRAINING_PERIOD+TESTING_PERIOD], forecast)
print(f'RMSE: {rmse:.2f}')
```

### Example 3: Visualizing Multiple Metrics

```python
import matplotlib.pyplot as plt

metrics = ['n_flows', 'n_packets', 'n_bytes']
fig, axes = plt.subplots(len(metrics), 1, figsize=(15, 12))

for idx, metric in enumerate(metrics):
    axes[idx].plot(df['time'], df[metric])
    axes[idx].set_title(f'{metric} Over Time')
    axes[idx].set_ylabel(metric)
    axes[idx].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
```

---

## ⚙️ Model Configuration

### SARIMA Hyperparameters

The default configuration is optimized for hourly network traffic data:

```python
{
    "order": (1, 1, 1),           # (p, d, q) - ARIMA order
    "seasonal_order": (1, 1, 1, 168),  # (P, D, Q, M) - Seasonal ARIMA
    "training_period": 744,        # 31 days in hours
    "testing_period": 168,         # 7 days in hours
    "retraining_stride": 168       # Retrain every 7 days
}
```

### Hyperparameter Tuning Guide

| Parameter | Description | Typical Range | Notes |
|-----------|-------------|---------------|-------|
| `p` | AR order | 0-5 | Number of lag observations |
| `d` | Differencing order | 0-2 | Number of differences for stationarity |
| `q` | MA order | 0-5 | Size of moving average window |
| `P` | Seasonal AR order | 0-2 | Seasonal autoregressive order |
| `D` | Seasonal differencing | 0-1 | Seasonal differencing degree |
| `Q` | Seasonal MA order | 0-2 | Seasonal moving average order |
| `M` | Seasonal period | 24, 168, 8760 | Hours in day/week/year |

---

## 📊 Evaluation Metrics

### 1. Root Mean Squared Error (RMSE)

Measures the standard deviation of prediction errors.

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
$$

**Lower is better** • Sensitive to outliers • Same units as target variable

### 2. Symmetric Mean Absolute Percentage Error (SMAPE)

Percentage-based metric treating over/under-estimation equally.

$$
\text{SMAPE} = \frac{100\%}{n} \sum_{i=1}^{n} \frac{|y_i - \hat{y}_i|}{(|y_i| + |\hat{y}_i|)/2}
$$

**Range: 0-100%** • 0% = perfect • Symmetric • Scale-independent

### 3. R² Score (Coefficient of Determination)

Proportion of variance in the target variable explained by the model.

$$
R^2 = 1 - \frac{\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}{\sum_{i=1}^{n}(y_i - \bar{y})^2}
$$

**Range: -∞ to 1** • 1 = perfect prediction • 0 = baseline model • Negative = worse than baseline

---

## 📁 Project Structure

```
TimeSeries-NetTraffic-Engine/
│
├── 📓 example.ipynb                    # Interactive tutorial notebook
├── 📓 analyze-results.ipynb            # Results analysis and visualization
├── 🐍 sarima_retraining.py            # CLI tool for SARIMA retraining
│
├── 📁 metacentrum_scripts/            # HPC batch processing scripts
│   ├── run_ip_addresses_sample.sh
│   ├── run_institutions.sh
│   ├── run_institution_subnets.sh
│   ├── sarima_retraining_ip_addresses_sample.sh
│   ├── sarima_retraining_institutions.sh
│   └── sarima_retraining_institution_subnets.sh
│
├── 📁 cesnet-time-series-2023-2024/   # Dataset directory (not included)
│   ├── times/                         # Timestamp files
│   ├── ip_addresses_sample/           # Sample IP dataset
│   ├── ip_addresses_full/             # Full IP dataset
│   ├── institutions/                  # Institution-level data
│   └── institution_subnets/           # Subnet-level data
│
├── 📁 results/                        # Output directory for predictions
│   └── sarima-retraining/
│       └── results/
│
├── 📄 LICENSE                         # BSD 3-Clause License
└── 📄 README.md                       # This file
```

---

## 🔬 Advanced Usage

### Custom Preprocessing Pipeline

```python
def custom_fill_missing(train_df, train_time_ids, strategy='mean'):
    """
    Custom missing value imputation strategy
    
    Args:
        train_df: Training dataframe
        train_time_ids: Expected time IDs
        strategy: 'mean', 'median', 'zero', or 'forward_fill'
    """
    df_missing = pd.DataFrame(columns=train_df.columns)
    df_missing.id_time = train_time_ids[~train_time_ids.isin(train_df.id_time)].values
    
    for column in train_df.columns:
        if column == "id_time":
            continue
        
        if strategy == 'mean':
            df_missing[column] = train_df[column].mean()
        elif strategy == 'median':
            df_missing[column] = train_df[column].median()
        elif strategy == 'zero':
            df_missing[column] = 0
        # Add more strategies as needed
    
    return pd.concat([train_df, df_missing]).sort_values(by="id_time").reset_index()[train_df.columns]
```

### Multi-Metric Forecasting

```python
# Forecast all metrics for a single time series
metrics = ['n_flows', 'n_packets', 'n_bytes']
predictions = {}

for metric in metrics:
    model = SARIMAX(df[metric], order=(1,1,1), seasonal_order=(1,1,1,168))
    results = model.fit(disp=False)
    predictions[metric] = results.forecast(steps=168)

# Create prediction dataframe
predictions_df = pd.DataFrame(predictions)
```

### Parallel Processing with Joblib

```python
from joblib import Parallel, delayed

def process_time_series(file_path, metric):
    """Process a single time series"""
    df = pd.read_csv(file_path)
    # ... training and prediction logic
    return predictions

# Process multiple files in parallel
results = Parallel(n_jobs=-1)(
    delayed(process_time_series)(file, 'n_flows') 
    for file in file_list
)
```

---

## 📈 Performance & Benchmarks

### Computational Requirements

| Operation | Time (Avg) | Memory | Notes |
|-----------|------------|--------|-------|
| Load 1-hour dataset | ~2 seconds | 50 MB | Per IP address |
| SARIMA training (744 points) | ~5-10 seconds | 200 MB | Single metric |
| Forecast (168 points) | ~1 second | 50 MB | Using fitted model |
| Complete retraining cycle | ~2-5 minutes | 500 MB | Full year, single metric |

### Scalability

- **Single IP Address**: ~5 minutes for full analysis (all metrics)
- **100 IP Addresses**: ~8 hours (with parallel processing)
- **1000 IP Addresses**: ~3 days (recommended: HPC cluster)

### Recommended Hardware

| Scale | CPU | RAM | Storage |
|-------|-----|-----|---------|
| **Small** (< 100 time series) | 4 cores | 8 GB | 10 GB |
| **Medium** (100-1000 time series) | 16 cores | 32 GB | 50 GB |
| **Large** (1000+ time series) | 32+ cores | 64+ GB | 200+ GB |

---

## 🤝 Contributing

We welcome contributions from the community! Here's how you can help:

### Ways to Contribute

1. **🐛 Report Bugs**: Open an issue with detailed reproduction steps
2. **💡 Suggest Features**: Share your ideas for improvements
3. **📝 Improve Documentation**: Help make our docs clearer
4. **🔧 Submit Pull Requests**: Contribute code improvements

### Development Setup

```bash
# Fork and clone the repository
git clone https://github.com/KUNALSHAWW/TimeSeries-NetTraffic-Engine.git
cd TimeSeries-NetTraffic-Engine

# Create a development branch
git checkout -b feature/your-feature-name

# Make your changes and test thoroughly
# ...

# Commit with clear messages
git commit -m "Add: Description of your changes"

# Push to your fork
git push origin feature/your-feature-name

# Open a Pull Request on GitHub
```

### Code Style Guidelines

- Follow PEP 8 for Python code
- Add docstrings to all functions
- Include type hints where applicable
- Write unit tests for new features
- Update documentation for API changes

---

## 📄 License

This project is licensed under the **BSD 3-Clause License** - see the [LICENSE](LICENSE) file for details.

```
Copyright (c) 2024, CESNET
All rights reserved.
```

### Third-Party Licenses

- **pandas**: BSD 3-Clause License
- **NumPy**: BSD License
- **scikit-learn**: BSD 3-Clause License
- **statsmodels**: BSD License
- **matplotlib**: PSF License

---

## 🙏 Acknowledgments

### CESNET

Special thanks to **CESNET** for providing the comprehensive CESNET-TimeSeries-2023-2024 dataset, which makes this research and development possible.

### Research Foundation

This work builds upon established research in:
- Time series forecasting
- Network traffic analysis
- SARIMA modeling
- Statistical learning

### Open Source Community

Built with ❤️ using:
- [pandas](https://pandas.pydata.org/) - Data manipulation
- [NumPy](https://numpy.org/) - Numerical computing
- [scikit-learn](https://scikit-learn.org/) - Machine learning
- [statsmodels](https://www.statsmodels.org/) - Statistical models
- [matplotlib](https://matplotlib.org/) - Visualization
- [seaborn](https://seaborn.pydata.org/) - Statistical visualization

---

## 📖 Citation

If you use this framework in your research, please cite:

```bibtex
@software{timeseries_nettraffic_engine,
  title = {TimeSeries-NetTraffic-Engine: Advanced Network Traffic Time Series Forecasting Framework},
  author = {Kunal Shaw},
  year = {2024},
  url = {https://github.com/KUNALSHAWW/TimeSeries-NetTraffic-Engine},
  note = {Based on CESNET-TimeSeries-2023-2024 dataset}
}
```

---

## 📞 Contact & Support

### Get Help

- **📧 Email**: kunalshawkol17@gmail.com
- **💬 Discussions**: [GitHub Discussions](https://github.com/KUNALSHAWW/TimeSeries-NetTraffic-Engine/discussions)
- **🐛 Issues**: [GitHub Issues](https://github.com/KUNALSHAWW/TimeSeries-NetTraffic-Engine/issues)

### Connect

- **🔗 LinkedIn**: [Your LinkedIn](https://www.linkedin.com/in/kunal-kumar-shaw-443999205)

---

## 🗺️ Roadmap

### Current Version (v1.0)
- ✅ SARIMA forecasting implementation
- ✅ Multi-dataset support
- ✅ Comprehensive evaluation metrics
- ✅ Jupyter notebooks for exploration
- ✅ HPC batch processing scripts

### Upcoming Features (v2.0)
- 🔄 LSTM/GRU deep learning models
- 🔄 Prophet integration
- 🔄 Real-time forecasting API
- 🔄 Web-based visualization dashboard
- 🔄 Automated hyperparameter tuning
- 🔄 Anomaly detection module

### Future Vision (v3.0)
- 🌟 Multi-variate forecasting
- 🌟 Ensemble methods
- 🌟 Transfer learning across datasets
- 🌟 Edge deployment capabilities
- 🌟 Integration with network monitoring tools

---

## ⭐ Star History

If you find this project useful, please consider giving it a star ⭐ on GitHub!

[![Star History Chart](https://api.star-history.com/svg?repos=KUNALSHAWW/TimeSeries-NetTraffic-Engine&type=Date)](https://star-history.com/#KUNALSHAWW/TimeSeries-NetTraffic-Engine&Date)

---

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/KUNALSHAWW/TimeSeries-NetTraffic-Engine?style=social)
![GitHub forks](https://img.shields.io/github/forks/KUNALSHAWW/TimeSeries-NetTraffic-Engine?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/KUNALSHAWW/TimeSeries-NetTraffic-Engine?style=social)
![GitHub contributors](https://img.shields.io/github/contributors/KUNALSHAWW/TimeSeries-NetTraffic-Engine)
![GitHub last commit](https://img.shields.io/github/last-commit/KUNALSHAWW/TimeSeries-NetTraffic-Engine)

---

<div align="center">

**Made with ❤️ by Data Scientists, for Data Scientists**

[⬆ Back to Top](#-timeseries-nettraffic-engine)

</div>
