# Real-Time Cluster-Level Resource Prediction Framework

---

## A Novel Approach to Cloud Resource Analysis

As a student deeply engaged with the complexities of cloud infrastructure, I've observed a recurring challenge: the sheer volume of low-level, machine-centric telemetry often obscures the bigger picture of resource consumption. This project aims to bridge that gap by offering a **fundamentally different perspective** on resource utilization. Instead of focusing on individual physical hosts or granular microservice instances, this framework and its accompanying dataset aggregate data at the **resource pool level**. This abstraction is critical for anyone performing high-level capacity planning, optimizing virtualized environments, or developing intelligent resource scheduling algorithms.

This repository presents a **real-time framework for cluster-level resource prediction, leveraging advanced learning techniques to optimize cloud efficiency.**

---

## Why This Framework is Pertinent and Innovative

Existing open datasets and frameworks frequently provide machine-level or task-level utilization metrics. While invaluable for specific performance tuning or debugging, they can lead to an analytical "tree-for-the-forest" problem when addressing macroscopic infrastructure concerns. Our framework's innovation lies in its **resource pool-centric organization** and the advanced predictive models, offering distinct advantages for professional analysis:

* **Elevated Abstraction for Strategic Planning:** By consolidating metrics at the pool level, we empower analysts to understand aggregate consumption patterns across logical resource groupings. This view is indispensable for strategic capacity planning, budget allocation, and inter-departmental resource negotiation in large-scale cloud deployments.
* **Enhanced Visibility for Anomaly Detection:** Identifying anomalous behavior within a single machine's metrics is one thing; detecting an unexpected surge or dip across an entire pool—indicative of a broader system event or misconfiguration—is another. This framework facilitates anomaly detection at a more impactful, operational level.
* **Foundation for Advanced Resource Orchestration:** Understanding pool-level utilization dynamics provides crucial input for developing and validating advanced resource orchestration algorithms, auto-scaling mechanisms, and intelligent load-balancing strategies within virtualized and containerized environments.
* **Reduced Data Granularity Overhead:** While fine-grained data has its place, aggregating at the pool level can significantly reduce the computational overhead for certain types of analysis, allowing for quicker insights into overall system health and trends.

---

## Dataset Architecture and Usage Protocol

The accompanying dataset (which forms the basis for this framework) is intuitively structured, with each top-level directory representing a distinct **resource pool**. Within these directories, data is further segmented by temporal granularity.

### Monthly Aggregates: `cluster-dataseries-cpu-mem` (For Trend Analysis & Model Training)

These files provide a monthly aggregation of resource usage, ideal for long-term trend analysis, forecasting, and training predictive models.

* **Naming Convention:** Files adhere to the `cluster-dataseries-cpu-mem_YYYY-MM.csv` format (e.g., `cluster-dataseries-cpu-mem_2023-01.csv`).
* **Temporal Granularity:** Monthly, providing a consolidated view of usage across the entire month.
* **Key Columns for Analysis:** Each file contains five columns. For most analytical tasks, the following two are paramount:
    * **Column 2 (Timestamp):** Represents the data point's time, typically in Unix epoch format.
    * **Column 4 (CPU Usage):** The normalized CPU utilization for the resource pool during that time interval.

### Daily Test Samples: `test-dataseries-daily` (For Validation & Quick Iterations)

This subset offers daily, more granular data suitable for validating hypotheses, rapid prototyping of analytical models, and observing shorter-term fluctuations.

* **Naming Convention:** Files are named `test-dataseries-daily_YYYY-MM-DD.csv` (e.g., `test-dataseries-daily_2023-01-15.csv`).
* **Temporal Granularity:** Daily, offering a more detailed look at daily variations.
* **Key Columns:** These files are streamlined to two essential columns:
    * **Column 1 (Timestamp):** The time of the data point.
    * **Column 2 (CPU Usage):** The corresponding CPU utilization.

---

## Quick Start & Practical Application

To leverage this dataset, simply access the desired resource pool directory and load the relevant `.csv` files. Below is a Python snippet using the `pandas` library, demonstrating how to extract the crucial columns:

```python
import pandas as pd

# Example: Loading a monthly aggregate for a hypothetical 'production_pool'
# Ensure you replace 'your_resource_pool_name' and 'YYYY-MM' with your specific folder and month
monthly_file_path = 'your_resource_pool_name/cluster-dataseries-cpu-mem_2023-01.csv'
df_monthly = pd.read_csv(monthly_file_path, header=None)

# Extracting the timestamp (Column 2) and CPU Usage (Column 4)
timestamp_monthly = df_monthly.iloc[:, 1]
cpu_usage_monthly = df_monthly.iloc[:, 3]

print(f"Sample of Monthly CPU Usage from {monthly_file_path}:\n{cpu_usage_monthly.head()}")

# ---

# Example: Loading a daily test sample for the same 'production_pool'
# Replace '2023-01-15' with your specific date
daily_file_path = 'your_resource_pool_name/test-dataseries-daily_2023-01-15.csv'
df_daily = pd.read_csv(daily_file_path, header=None)

# Extracting the timestamp (Column 1) and CPU Usage (Column 2)
timestamp_daily = df_daily.iloc[:, 0]
cpu_usage_daily = df_daily.iloc[:, 1]

print(f"\nSample of Daily CPU Usage from {daily_file_path}:\n{cpu_usage_daily.head()}")
