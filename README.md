## Real-Time Cluster Resource Prediction Framework

This repository hosts an open dataset of cloud resource clusters structured from a **Resource Pool** perspective, along with a prediction framework designed to streamline the workflow from raw telemetry to high-level capacity planning and scheduling algorithm development.

---

### 1. Overview

Traditional cloud monitoring datasets often focus on machine-level or service-level metrics (e.g., physical servers or individual containers), overlooking the macro usage patterns at the **Cluster Pool** level. In this project, raw monitoring data is organized by resource pool, emphasizing **Cluster-Level** resource utilization for each pool:

- **Directory Structure**: Each top-level folder under the repo root represents one resource pool (a logical cluster).
- **Naming Conventions**:
  - **Monthly Aggregates**: `<pool_name>/cluster-dataseries-cpu-mem-YYYYMM_0.csv` for long-term trend analysis and model training.
  - **Daily Test Samples**: `<pool_name>/test-dataseries-daily-YYYY-MM-DD.csv` for model validation and rapid prototyping.

---

### 2. Dataset Schema

All CSV files are **headerless** (`header=None`) and contain at least four columns:

| Column Index | Description   | Details                           |
| ------------ | ------------- | --------------------------------- |
| 0            | Cluster Name  | String identifier of the pool     |
| 1            | Timestamp     | Datetime in format YYYY-MM-DD HH:MM:SS    |
| 2            | —             | Irrelevant for modeling |
| 3            | CPU Usage     | Raw CPU usage value for the pool at the timestamp |

---

### 3. Quick Start

The following `pandas` snippet demonstrates loading routines for training and testing phases.

```python
import pandas as pd

# Assume file_list contains paths to CSV files, e.g.:
# file_list = ['cluster1/cluster-dataseries-cpu-mem-202407_0.csv', ...]

if arg.is_training:
    # Training: read only Timestamp and CPU Usage columns
    dataset = [pd.read_csv(file_name, usecols=[1, 3], names=['timestamp', 'cpu(u)']) for file_name in file_list] # Select 2nd (timestamp) and 4th (CPU)
else:
    # Testing: files contain only two columns (Timestamp, CPU Usage)
    dataset = [pd.read_csv(file_name, names=['timestamp', 'cpu(u)']) for file_name in file_list]

---

### 4. Highlights & Use Cases
4. Highlights & Use Cases

- **Pool-Level Perspective**: Focused on cluster-level resources, ideal for macro capacity planning and auto-scaling algorithm evaluation.

- **Ease of Use**: Unified directory and file naming enable batch loading and preprocessing of key fields with minimal code.

- **Real-Time Prediction**: Integrates seamlessly with any deep learning or time-series model for short-term load forecasting and dynamic scaling.

Extend this foundation with additional metrics (e.g., memory, network) or combine with business KPIs to build more sophisticated cloud resource orchestration solutions.

Contact

If you have any questions or want to use the code, feel free to contact: [your-email@example.com]
