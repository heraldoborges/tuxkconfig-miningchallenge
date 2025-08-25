# TuxKConfig Mining Challenge Repository

## Overview
This repository supports the TuxKConfig dataset for the MSR 2026 Mining Challenge. TuxKConfig is a comprehensive collection of 243,232 valid Linux kernel configurations for the x86_64 architecture, systematically sampled across seven major releases (versions 4.13, 4.15, 4.20, 5.0, 5.4, 5.7, and 5.8). It includes high-dimensional binary vectors for configuration options (e.g., CONFIG_PCI) and key non-functional properties like uncompressed vmlinux binary size (in MB), compressed kernel image sizes (e.g., GZIP, XZ), and compilation time (in seconds).

The dataset enables research on performance prediction, temporal dynamics of software configuration spaces, evolution analysis, feature interactions, transfer learning, and more. It captures three years of Linux evolution and is designed for the MSR challenge to allow participants to apply mining tools on a shared real-world dataset. The dataset is publicly and permanently hosted on OpenML (aggregator ID: 46749; [link to OpenML](https://www.openml.org/d/46749)), ensuring accessibility without credentials. For the foundational datapaper, see ["Linux Kernel Configurations at Scale: A Dataset for Performance and Evolution Analysis" (EASE 2025)](https://hal.science/hal-05063560v1/document).

## Objectives
The challenge aims to showcase techniques, tools, and creativity in mining the TuxKConfig dataset. Participants are encouraged to address one or more of the proposed challenges, focusing on machine learning, software evolution, and configurable systems.

## Dataset Overview
TuxKConfig addresses gaps in existing datasets by providing a large-scale, multi-version collection of Linux kernel configurations. It was constructed using tools like TuxML for automated configuration generation (via `make randconfig`), compilation, and measurement in a Docker environment on clusters. Configurations are valid and respect Kconfig dependencies.

Key characteristics:
- **Creators**: Heraldo Borges, Juliana Alves Pereira, Djamel Eddine Khelladi, Mathieu Acher.
- **Versions Covered**: 4.13 (September 2017) to 5.8 (August 2020), reflecting milestones like security enhancements and large updates.
- **Total Instances (Configurations)**: 243,232.
- **Attributes (Features)**: Varies by version (9,445 to 12,502 binary-encoded tristate options); plus target variables like vmlinux size, compilation time, and derived features (e.g., Sum_Enabled_Options).
- **Format**: Tabular data in CSV files (one per version), compressed to ~2 GB total.
- **Tags/Keywords**: Configurable Systems, Linux Kernel, Kernel Configuration, Tabular Data, Software Evolution.
- **Preprocessing**: Binarization of tristate options ('y'=1, 'n'/'m'=0), removal of non-tristate and constant options, addition of derived features.
- **Measurements**: vmlinux (uncompressed binary size in MB), compressed sizes (e.g., GZIP-vmlinux), compilation time (hardware-dependent, averaged ~261 seconds on 16-core machines).

The following table summarizes characteristics per version (from the EASE datapaper):

| Version | Options | Configurations | Min/Max Size (MB) |
|---------|---------|----------------|-------------------|
| 4.13   | 12,502 | 92,471         | 7.0 / 1698.1     |
| 4.15   | 9,445  | 39,391         | 11.0 / 1783.8    |
| 4.20   | 10,209 | 23,489         | 11.0 / 2035.5    |
| 5.0    | 10,313 | 19,952         | 11.0 / 1869.5    |
| 5.4    | 10,833 | 25,847         | 11.1 / 1959.4    |
| 5.7    | 11,358 | 20,159         | 11.1 / 1906.0    |
| 5.8    | 11,550 | 21,923         | 11.1 / 1905.1    |


## Accessing the Dataset
The full dataset is available on OpenML for direct download or programmatic access. No authentication is required.

- **Aggregator Dataset**: ID 46749 (links all versions).
- **Individual Versions**: 
  - 4.13 (ID 46738)
  - 4.15 (ID 46739)
  - 4.20 (ID 46740)
  - 5.0 (ID 46741)
  - 5.4 (ID 46742)
  - 5.7 (ID 46743)
  - 5.8 (ID 46744)

**Recommended Access Method**: Use the `openml-python` library to load data directly into Python.

Example code to load a version (e.g., 5.8):
```python
import openml
import pandas as pd

# Load dataset
dataset = openml.datasets.get_dataset(46744)  # Version 5.8
X, y, categorical_indicator, attribute_names = dataset.get_data(
    target=dataset.default_target_attribute, dataset_format="dataframe"
)
