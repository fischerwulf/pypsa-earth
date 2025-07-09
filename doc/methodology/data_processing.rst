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

    ┌───────────────────────────────────────────────────────────────────────────────────────┐
    │                           PyPSA-Earth Data Processing Pipeline                        │
    └───────────────────────────────────────────────────────────────────────────────────────┘
    
    INPUT DATA SOURCES                PROCESSING MODULES                    MODEL OUTPUTS
    ┌─────────────────┐             ┌─────────────────┐                   ┌─────────────────┐
    │ Weather Data    │             │ Renewable       │                   │ Energy System   │
    │ • ERA5          │  ───────►   │ Resource        │  ──────────┐      │ Components      │
    │ • SARAH-2       │             │ Assessment      │            │      │ • Generators    │
    │ • GEBCO         │             └─────────────────┘            │      │ • Transmission  │
    └─────────────────┘                                            │      │ • Storage       │
                                                                   │      │ • Load Centers  │
    ┌─────────────────┐             ┌─────────────────┐            │      └─────────────────┘
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

Renewable Energy Resource Assessment
------------------------------------

**Overview**: The renewable energy resource assessment transforms meteorological data into technology-specific renewable energy potentials and generation time series for wind, solar, and hydro technologies.

**Implementation Approach**: 

Weather data from reanalysis databases undergoes spatial and temporal processing to generate technology-specific capacity factors. The workflow integrates land use constraints and applies spatial optimization techniques to determine realistic installation potentials while maintaining high temporal resolution for energy system modeling.

**Key Components**:

- **Atlite Weather Processing**: Fifth European Centre for Medium-Range Weather Forecasts (ECMWF) Reanalysis (ERA5) and Surface Solar Radiation Data Set - Heliosat (SARAH-2) satellite data processing through the `Atlite package <https://github.com/PyPSA/atlite>`_
- **Technology Conversion**: Wind, solar, and hydro resource assessment with technology-specific generation curves
- **Land Use Integration**: `Copernicus land cover data <https://land.copernicus.eu/global/products/lc>`_ for siting constraints and protected area exclusions
- **Spatial Optimization**: Generation density applications and grid cell-level resource aggregation

**Main Outputs**: Hourly renewable energy capacity factors, maximum installable capacities, and spatial resource maps

**Data Flow**: Weather data → Atlite cutouts → Technology conversion → Spatial aggregation → Time series generation

.. image:: /img/offwinddc-gridcell.png
    :width: 45%
    :align: left
    :alt: Offshore Wind DC Grid Cell Analysis

.. image:: /img/solar-gridcell.png
    :width: 45%
    :align: right
    :alt: Solar Photovoltaic (PV) Grid Cell Analysis

*Figure: Example renewable resource processing showing offshore wind and solar PV grid cell analysis*

Energy Demand Modeling
----------------------

**Overview**: The energy demand modeling component generates spatially and temporally disaggregated electricity demand profiles using socio-economic indicators and machine learning approaches.

**Implementation Approach**: 

Socio-economic data including population, economic activity, and climate variables serve as inputs for machine learning models that predict electricity demand patterns. The approach combines historical validation with scenario-based projections to support both current and future energy system planning.

**Key Components**:

- **Global Energy GIS (GEGIS) Integration**: Machine learning-based demand prediction using `Global Energy GIS package <https://github.com/niclasmattsson/GlobalEnergyGIS>`_
- **Synde Workflow**: Automated data acquisition, preprocessing, and quality control via `Synde <https://github.com/euronion/synde>`_
- **Shared Socioeconomic Pathways (SSP) Scenario Integration**: Future demand projections under different socio-economic pathways (2030-2100)
- **Multi-Variable Modeling**: Temperature, population, Gross Domestic Product (GDP), and sectoral activity as demand drivers

**Main Outputs**: Hourly electricity demand time series at sub-national resolution, future demand scenarios

**Data Flow**: Socio-economic data → Machine learning training → Validation → Demand time series → Scenario projections

**Validation Performance**: 8% average error across 44 countries with continuous improvement frameworks

Infrastructure and Network Data Processing
------------------------------------------

**Overview**: The infrastructure and network data processing component transforms geographic and infrastructure information into network topology and spatial constraints for energy system modeling.

**Implementation Approach**: 

Geographic databases and infrastructure repositories are processed to extract network topology, administrative boundaries, and spatial constraints. The workflow harmonizes different data sources while maintaining spatial consistency across all processed outputs.

**Key Components**:

- **OpenStreetMap (OSM) Processing**: Extraction and cleaning of infrastructure data from `OpenStreetMap <https://www.openstreetmap.org/>`_
- **Administrative Boundaries**: Integration of geographic boundaries and administrative regions using `Natural Earth <https://www.naturalearthdata.com/>`_ and `GADM <https://gadm.org/>`_ datasets
- **Land Use Constraints**: Protected areas, urban zones, and other exclusion criteria from `World Database on Protected Areas <https://www.protectedplanet.net/>`_
- **Maritime Boundaries**: Offshore resource areas and exclusive economic zones from `Marine Regions <https://www.marineregions.org/>`_

**Main Outputs**: Network node locations, transmission line data, spatial boundary definitions

**Integration Point**: Coordinates with :doc:`network_modeling` for complete topology creation


Data Integration and Quality Assurance
====================================

Integration Architecture
------------------------

The three data processing streams are integrated through a coordinated quality assurance framework that ensures consistency and reliability across all model inputs. The integration maintains both spatial and temporal coherence while enabling modular processing workflows.

**Implementation Approach**:

Spatial and temporal synchronization mechanisms ensure that all data streams produce compatible outputs for energy system modeling. The architecture supports both current year analyses and future scenario projections while maintaining data quality standards throughout the processing pipeline.

**Spatial Consistency Framework**:

- **Common Coordinate Systems**: All data processing uses consistent geographic projections (World Geodetic System 1984, WGS84)
- **Boundary Alignment**: Administrative regions, network nodes, and resource areas are spatially synchronized
- **Resolution Harmonization**: Different data resolutions are reconciled through appropriate aggregation/disaggregation methods

**Temporal Synchronization**:

- **Common Time References**: All time series are aligned to Coordinated Universal Time (UTC) with consistent temporal resolution
- **Weather Year Coordination**: Renewable resources, demand patterns, and operational constraints use synchronized meteorological years
- **Scenario Timeline Alignment**: Future projections maintain temporal consistency across all data streams

Quality Assurance Framework
---------------------------

**Overview**: The quality assurance framework implements multi-level validation procedures to ensure data reliability and physical consistency across all processing streams.

**Implementation Approach**:

Validation procedures operate at multiple stages of the data processing pipeline, from initial data quality assessment through final model input verification. The framework includes both automated quality checks and manual validation procedures.

**Multi-Level Validation Approach**:

1. **Input Data Validation**: Raw data quality assessment and cleaning procedures
2. **Processing Validation**: Intermediate result verification during transformation steps  
3. **Output Validation**: Final model input verification against known benchmarks
4. **Integration Validation**: Cross-component consistency checks and energy balance verification


Implementation Documentation
============================

**Code Implementation**: Data processing modules are implemented in the `scripts/ directory <https://github.com/pypsa-meets-earth/pypsa-earth/tree/main/scripts>`_ with full documentation and example configurations. The modules provide both command-line interfaces and programmatic access for integration into larger workflows.

**Reproducibility**: All processing steps are version-controlled and documented to ensure reproducible research workflows. Configuration files and processing parameters are maintained in the `PyPSA-Earth repository <https://github.com/pypsa-meets-earth/pypsa-earth>`_ to support reproducible research and collaborative development.

Integration with PyPSA Model Formulation
========================================

**Overview**: The processed data serves as the foundation for PyPSA network model formulation, which is subsequently solved using linear programming optimization techniques.

**From Data Processing to Model Formulation**:

The comprehensive data processing pipeline described in this document creates the essential inputs for PyPSA-Earth's energy system optimization models. The three main data processing streams converge to provide:

1. **Technology Parameters**: Renewable energy potentials and generation time series become capacity constraints and availability factors in the optimization model
2. **System Topology**: Network infrastructure data defines the spatial structure, transmission capacities, and connectivity constraints
3. **Demand Profiles**: Spatially and temporally resolved electricity demand serves as the load balance requirements

**Model Integration Workflow**:

.. code-block:: text

     DATA PROCESSING OUTPUTS          ──►   PYPSA MODEL COMPONENTS
    ┌──────────────────────────────┐       ┌─────────────────────────────┐
    │ • Renewable capacity factors │  ──►  │ • Generator objects         │
    │ • Maximum installable caps   │       │ • Marginal costs            │
    │ • Hourly time series         │       │ • Efficiency parameters     │
    └──────────────────────────────┘       └─────────────────────────────┘
    
    ┌──────────────────────────────┐       ┌─────────────────────────────┐
    │ • Network topology data      │  ──►  │ • Bus definitions           │
    │ • Transmission line specs    │       │ • Line capacity constraints │
    │ • Spatial boundaries         │       │ • Impedance parameters      │
    └──────────────────────────────┘       └─────────────────────────────┘
    
    ┌──────────────────────────────┐       ┌─────────────────────────────┐
    │ • Hourly demand profiles     │  ──►  │ • Load time series          │
    │ • Spatial demand allocation  │       │ • Bus load assignments      │
    │ • Scenario projections       │       │ • Demand response options   │
    └──────────────────────────────┘       └─────────────────────────────┘

**Mathematical Integration**: The processed data integrates into PyPSA's linear programming formulation through specific parameter mappings that ensure physical consistency and computational tractability. Detailed mathematical formulations are provided in :doc:`mathematical_framework`.

**Optimization and Solving**: Once the PyPSA network model is populated with processed data, it undergoes optimization using linear programming solvers to minimize total system costs while satisfying all technical and operational constraints. The solving process and available solution methods are documented in :doc:`../solving`.

References and Further Reading
====================================

**Technical Implementation Details:**

* :doc:`../populate_data` - Detailed technical specifications for data processing algorithms and computational optimization methods
* :doc:`../tutorial_electricity` - Step-by-step implementation examples with technical configuration details
* :doc:`../configuration` - Advanced configuration options and parameter settings for all processing components

**Mathematical Formulations:**

* :doc:`mathematical_framework` - Mathematical representation of optimization constraints and how processed data integrates with energy system models
* :doc:`../costs` - Cost data processing and economic parameter integration methods

**Validation and Quality Control:**

* :doc:`validation_framework` - Comprehensive validation procedures, uncertainty quantification methods, and statistical quality control approaches
* :doc:`../customization_validation` - Custom validation workflows and performance benchmarking procedures

**Workflow Integration:**

* :doc:`workflow_management` - Snakemake workflow implementation, computational performance optimization, and automated processing pipelines
* :doc:`network_modeling` - Integration with network topology processing and spatial data handling workflows

**Data Source Specifications:**

* :doc:`data_sources` - Comprehensive data source documentation with access methods, quality specifications, and processing requirements

**Open Source Tools and Repositories:**

- `Atlite <https://github.com/PyPSA/atlite>`_ - Renewable energy time series and potential calculation
- `PyPSA <https://github.com/PyPSA/PyPSA>`_ - Python for Power System Analysis framework
- `GEGIS <https://github.com/niclasmattsson/GlobalEnergyGIS>`_ - Global Energy GIS for demand modeling
- `Synde <https://github.com/euronion/synde>`_ - Synthetic demand generation workflow
- `powerplantmatching <https://github.com/PyPSA/powerplantmatching>`_ - Power plant data matching and validation