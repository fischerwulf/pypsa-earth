.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _data_processing:

##########################################
Data Processing
##########################################

Overview
========

PyPSA-Earth's data processing pipeline transforms heterogeneous open-source data into consistent, model-ready inputs for energy system optimization. This section provides an overview of how different data processing components work together to create spatially and temporally resolved energy system representations.

**Core Data Processing Philosophy:**

The pipeline follows a **modular, automated approach** that processes different data types through specialized workflows while maintaining consistency and quality across all outputs. Three main data streams converge to create the final energy system model:

1. **Weather and Resource Data** → Renewable energy potentials and time series
2. **Socio-Economic Data** → Energy demand patterns and development scenarios
3. **Geographic and Infrastructure Data** → Network topology and spatial constraints  

**Integrated Workflow Architecture:**

.. code-block:: text

    ┌──────────────────────────────────────────────────────────────────────────────────────┐
    │                           PyPSA-Earth Data Processing Pipeline                       │
    └──────────────────────────────────────────────────────────────────────────────────────┘
    
    INPUT DATA SOURCES                PROCESSING MODULES                    MODEL OUTPUTS
    ┌─────────────────┐             ┌─────────────────┐                  ┌─────────────────┐
    │ Weather Data    │             │ Renewable       │                  │ Energy System   │
    │ • ERA5          │  ───────►   │ Resource        │  ──────────┐     │ Components      │
    │ • SARAH-2       │             │ Assessment      │            │     │ • Generators    │
    │ • GEBCO         │             └─────────────────┘            │     │ • Transmission  │
    └─────────────────┘                                            │     │ • Storage       │
                                                                   │     │ • Load Centers  │
    ┌─────────────────┐             ┌─────────────────┐            │     └─────────────────┘
    │ Socio-Economic  │             │ Demand          │            ▼             │ 
    │ • Population    │  ───────►   │ Modeling        │  ──► ┌─────────┐         │
    │ • GDP           │             │ (GEGIS/Synde)   │      │ Data    │         │ 
    │ • SSP Scenarios │             └─────────────────┘      │ Fusion  │         │
    └─────────────────┘                                      │ &       │         ▼
                                                             │ Quality │  ┌─────────────────┐
    ┌─────────────────┐             ┌─────────────────┐      │ Control │  │ PyPSA Network   │
    │ Geographic Data │             │ Infrastructure  │  ──► └─────────┘  │ Model           │
    │ • OSM           │  ───────►   │ & Topology      │                   │ • .nc files     │
    │ • Administrative│             │ Processing      │                   │ • Time series   │
    │ • Land Use      │             └─────────────────┘                   │ • Parameters    │
    └─────────────────┘                                                   └─────────────────┘
                                                                          

**Key Integration Principles:**

- **Spatial Consistency**: All data processing maintains consistent geographic projections and administrative boundaries
- **Temporal Alignment**: Weather, demand, and operational data are synchronized to common time resolutions
- **Quality Assurance**: Multi-stage validation ensures data reliability and physical consistency
- **Modular Design**: Each processing component can be updated independently while preserving integration

Data Processing Components
==========================

The data processing pipeline consists of three main processing streams that work together to create comprehensive energy system inputs:

1. **Renewable Energy Resource Assessment**
------------------------------------------

**Purpose**: Transform meteorological data into technology-specific renewable energy potentials and generation time series.

**Key Components**:
- **Atlite Weather Processing**: ERA5 reanalysis and SARAH-2 satellite data processing through the Atlite package
- **Technology Conversion**: Wind, solar, and hydro resource assessment with technology-specific power curves
- **Land Use Integration**: Copernicus land cover data for siting constraints and protected area exclusions
- **Spatial Optimization**: Power density applications and grid cell-level resource aggregation

**Main Outputs**: Hourly renewable energy capacity factors, maximum installable capacities, and spatial resource maps

**Data Flow**: Weather data → Atlite cutouts → Technology conversion → Spatial aggregation → Time series generation

.. image:: /img/offwinddc-gridcell.png
    :width: 45%
    :align: left
    :alt: Offshore Wind DC Grid Cell Analysis

.. image:: /img/solar-gridcell.png
    :width: 45%
    :align: right
    :alt: Solar PV Grid Cell Analysis

*Figure: Example renewable resource processing showing offshore wind and solar PV grid cell analysis*

2. **Energy Demand Modeling**
----------------------------

**Purpose**: Generate spatially and temporally disaggregated electricity demand profiles using socio-economic drivers.

**Key Components**:
- **GEGIS Integration**: Machine learning-based demand prediction using Global Energy GIS package
- **Synde Workflow**: Automated data acquisition, preprocessing, and quality control
- **SSP Scenario Integration**: Future demand projections under different socio-economic pathways (2030-2100)
- **Multi-Variable Modeling**: Temperature, population, GDP, and sectoral activity as demand drivers

**Main Outputs**: Hourly electricity demand time series at sub-national resolution, future demand scenarios

**Data Flow**: Socio-economic data → Machine learning training → Validation → Demand time series → Scenario projections

**Validation Performance**: 8% average error across 44 countries with continuous improvement frameworks

3. **Infrastructure and Network Data Processing**
-----------------------------------------------

**Purpose**: Process geographic and infrastructure data to create network topology and spatial constraints.

**Key Components**:
- **OpenStreetMap Processing**: Extraction and cleaning of power infrastructure data
- **Administrative Boundaries**: Integration of geographic boundaries and administrative regions  
- **Land Use Constraints**: Protected areas, urban zones, and other exclusion criteria
- **Maritime Boundaries**: Offshore resource areas and exclusive economic zones

**Main Outputs**: Network node locations, transmission line data, spatial boundary definitions

**Integration Point**: Coordinates with :doc:`network_modeling` for complete topology creation


Data Integration and Quality Assurance
====================================

Integration Architecture
------------------------

The three data processing streams are integrated through a **coordinated quality assurance framework** that ensures consistency and reliability across all model inputs:

**Spatial Consistency Framework**:
- **Common Coordinate Systems**: All data processing uses consistent geographic projections (WGS84)
- **Boundary Alignment**: Administrative regions, network nodes, and resource areas are spatially synchronized
- **Resolution Harmonization**: Different data resolutions are reconciled through appropriate aggregation/disaggregation methods

**Temporal Synchronization**:
- **Common Time References**: All time series are aligned to UTC with consistent temporal resolution
- **Weather Year Coordination**: Renewable resources, demand patterns, and operational constraints use synchronized meteorological years
- **Scenario Timeline Alignment**: Future projections maintain temporal consistency across all data streams

**Cross-Validation Procedures**:
- **Physical Consistency Checks**: Energy balances, capacity constraints, and resource limits are validated
- **Multi-Source Verification**: Key parameters are cross-referenced against multiple independent data sources
- **Statistical Quality Control**: Outlier detection and error propagation analysis throughout the processing chain

Quality Assurance Framework
---------------------------

**Multi-Level Validation Approach**:

1. **Input Data Validation**: Raw data quality assessment and cleaning procedures
2. **Processing Validation**: Intermediate result verification during transformation steps  
3. **Output Validation**: Final model input verification against known benchmarks
4. **Integration Validation**: Cross-component consistency checks and energy balance verification

**Key Quality Metrics**:
- **Renewable Resource Validation**: Capacity factor distributions compared to literature values and operational data
- **Demand Model Accuracy**: 8% average error across 44 countries with regional performance tracking
- **Network Topology Verification**: Infrastructure data validation against official utility databases
- **Scenario Consistency**: SSP pathway alignment with published projections

**Uncertainty Quantification**:
- **Data Source Uncertainty**: Propagation of input data uncertainties through processing workflows
- **Model Parameter Uncertainty**: Sensitivity analysis for key processing parameters
- **Integration Uncertainty**: Assessment of compounding uncertainties across data streams

Computational Performance and Optimization
------------------------------------------

**Scalability Design**:
- **Modular Processing**: Independent processing streams allow parallel execution and selective updates
- **Memory Optimization**: Efficient data structures and streaming algorithms for large-scale global processing
- **Caching Strategies**: Intermediate result storage to minimize recomputation during iterative model development

**Processing Efficiency**:
- **Atlite Performance**: Optimized weather data processing with vectorized operations and multithreading
- **GEGIS Scalability**: Machine learning demand modeling with efficient training algorithms and prediction pipelines
- **Workflow Integration**: Snakemake coordination minimizes redundant processing and manages dependencies

Technical Documentation and Reproducibility
-------------------------------------------

**For detailed technical specifications, users should refer to**:

- **:doc:`../data_sources`** - Comprehensive data source documentation with access methods and quality specifications
- **:doc:`workflow_management`** - Snakemake workflow implementation and automation procedures  
- **:doc:`network_modeling`** - Integration with network topology processing and spatial data handling
- **:doc:`mathematical_framework`** - How processed data integrates with optimization formulations

**Code Implementation**: Data processing modules are implemented in the `scripts/` directory with full documentation and example configurations

**Reproducibility**: All processing steps are version-controlled and documented to ensure reproducible research workflows

References and Further Reading
==============================

**Primary References:**

* Parzen, M., et al. (2023). "PyPSA-Earth. A new global open energy system optimization model demonstrated in Africa." Applied Energy, 341, 121096.
* Hofmann, F., et al. (2021). "Atlite: A lightweight Python package for calculating renewable power potentials and time series." Journal of Open Source Software, 6(62), 3294.

**Data Sources:**

* ERA5 Reanalysis: Copernicus Climate Change Service
* SARAH-2 Solar Data: EUMETSAT Climate Monitoring SAF
* GEBCO Bathymetry: General Bathymetric Chart of the Oceans
* Copernicus Land Service: European Space Agency

**Related Documentation:**

* :doc:`network_modeling` - Network topology processing and construction
* :doc:`workflow_management` - Snakemake workflow automation
* :doc:`mathematical_framework` - Optimization formulations
* :doc:`../data_sources` - Detailed data source documentation
