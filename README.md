# realtime-cluster-prediction-framework
Resource Pool Utilization Dataset
This repository provides a novel dataset for analyzing resource utilization within cloud environments, distinctly categorized by resource pools rather than individual physical machines or microservices. This approach offers a macroscopic view of resource consumption, enabling more effective resource planning, anomaly detection, and capacity management at a higher level of abstraction.

Innovation and Uniqueness
Traditional datasets in this domain typically focus on individual task-level or microservice-level resource tracking on physical machines. While valuable, these granular datasets often obscure the overarching consumption patterns within larger infrastructure units. Our dataset introduces a paradigm shift by organizing data around resource pools. This provides several key advantages:

Holistic View: Gain insights into how entire resource pools are utilized, which is crucial for managing virtualized environments and cloud-native architectures.
Strategic Resource Management: Facilitates better understanding of resource allocation and potential bottlenecks across logical groupings of resources.
Enhanced Capacity Planning: Enables more accurate forecasting and planning based on aggregated pool-level consumption.
Simplified Anomaly Detection: Pinpoint unusual utilization patterns within a defined resource pool, making it easier to identify and address issues.
Dataset Structure and Usage
The dataset is organized into folders, with each folder representing a distinct resource pool.

Monthly Data (Training/Analysis)
File Naming Convention: Files starting with cluster-dataseries-cpu-mem
Granularity: Monthly
Columns: Each file contains five columns. For most analyses, you will primarily use:
Column 2: Timestamp (unix epoch or similar)
Column 4: CPU Usage (e.g., percentage or normalized value)
Daily Test Data
File Naming Convention: Files starting with test-dataseries-daily
Granularity: Daily
Columns: Each file contains two columns:
Timestamp (unix epoch or similar)
CPU Usage (e.g., percentage or normalized value)
