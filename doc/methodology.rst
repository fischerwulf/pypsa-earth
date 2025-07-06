.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _methodology:

##########################################
Methodology
##########################################

Mathematical Modeling Framework
===============================

PyPSA-Earth employs a linear programming approach for energy system optimization, building on the proven PyPSA framework. The mathematical formulation addresses the fundamental challenge of balancing energy supply and demand while minimizing system costs or emissions.

**Core Mathematical Formulation**

The optimization model minimizes total system costs:

.. math::

    \min \sum_{i,t} c_i \cdot g_{i,t} + \sum_{i} c_i^{inv} \cdot s_i

where:
- :math:`c_i` = operational costs of technology :math:`i`
- :math:`g_{i,t}` = generation/operation of technology :math:`i` at time :math:`t`
- :math:`c_i^{inv}` = investment costs of technology :math:`i`
- :math:`s_i` = capacity of technology :math:`i`

**Key Constraints**

1. **Energy Balance**: Supply must equal demand at each node and time step
2. **Technology Limits**: Generation cannot exceed installed capacity
3. **Transmission Constraints**: Power flows respect line capacity limits
4. **Ramping Constraints**: Technology-specific operational limitations
5. **Storage Dynamics**: Energy storage charge/discharge cycles

**Temporal and Spatial Resolution**

The model supports flexible temporal resolution from hourly to multi-year analysis. Spatial resolution ranges from administrative boundaries to substation-level detail. Advanced clustering algorithms reduce computational complexity while preserving essential system characteristics.

**Optimization Variants**

* **Operational Optimization**: Minimize costs for given infrastructure
* **Capacity Expansion**: Simultaneously optimize operation and investment
* **Multi-Objective**: Balance cost, emissions, and security objectives
* **Stochastic Programming**: Handle uncertainty in renewables and demand

Network Modeling Approach
=========================

PyPSA-Earth's network modeling combines automated data processing with sophisticated algorithms to create realistic representations of energy systems worldwide.

**Transmission Network Construction**

The framework automatically constructs transmission networks using:

1. **Substation Mapping**: Extract substation locations from OpenStreetMap
2. **Voltage Level Classification**: Categorize transmission lines by voltage
3. **Connection Algorithms**: Build realistic network topologies
4. **Line Parameter Estimation**: Calculate electrical parameters from geographic data

**Network Simplification**

For computational efficiency, the model employs several simplification strategies:

* **Busbar Aggregation**: Combine nearby substations into representative nodes
* **Line Bundling**: Represent parallel transmission lines as single equivalent lines
* **Clustering Algorithms**: Reduce network complexity while preserving key characteristics
* **Spatial Aggregation**: Generate networks at different resolution levels

**Power Flow Modeling**

The framework supports multiple power flow formulations:

* **DC Power Flow**: Linear approximation for large-scale optimization
* **AC Power Flow**: Non-linear formulation for detailed analysis
* **Hybrid Approaches**: Combine different formulations for specific applications

**Multi-Voltage Level Integration**

PyPSA-Earth models transmission, sub-transmission, and distribution networks:

* **Transmission (≥220 kV)**: High-voltage interconnections
* **Sub-transmission (35-220 kV)**: Regional distribution networks
* **Distribution (<35 kV)**: Local distribution systems

Data Processing Methodology
===========================

PyPSA-Earth's data processing pipeline transforms raw open-source data into model-ready inputs through automated workflows.

**Data Source Integration**

The framework integrates multiple data sources:

* **OpenStreetMap**: Infrastructure mapping and geographic data
* **Weather Databases**: Renewable energy resource assessment
* **Energy Statistics**: Demand patterns and generation data
* **Economic Data**: Cost assumptions and financial parameters

**Quality Assurance**

Comprehensive data validation ensures model reliability:

1. **Consistency Checks**: Verify data compatibility across sources
2. **Outlier Detection**: Identify and handle anomalous data points
3. **Gap Filling**: Interpolate missing data using statistical methods
4. **Validation Rules**: Apply domain-specific validation criteria

**Renewable Energy Modeling**

Advanced methods for renewable energy resource assessment:

* **Weather-to-Power Conversion**: Transform meteorological data to generation profiles
* **Capacity Factor Calculations**: Determine technology-specific performance
* **Spatial Aggregation**: Combine multiple weather points for regional profiles
* **Bias Correction**: Adjust for systematic errors in weather data

**Demand Modeling**

Sophisticated demand modeling captures consumption patterns:

* **Temporal Profiles**: Hourly, daily, and seasonal demand variations
* **Spatial Disaggregation**: Distribute national demand to regional nodes
* **Sector-Specific Patterns**: Residential, commercial, and industrial profiles
* **Temperature Dependence**: Model weather-sensitive demand components

Scenario Development Framework
=============================

PyPSA-Earth provides comprehensive tools for scenario analysis and uncertainty quantification.

**Scenario Definition**

Structured approach to scenario development:

* **Parameter Spaces**: Define ranges for key input parameters
* **Correlation Handling**: Manage dependencies between parameters
* **Constraint Variations**: Model different policy and technical constraints
* **Pathway Modeling**: Analyze transition dynamics over time

**Uncertainty Quantification**

Advanced methods for handling uncertainty:

* **Monte Carlo Sampling**: Generate multiple realizations of uncertain parameters
* **Sensitivity Analysis**: Identify key drivers of model results
* **Robust Optimization**: Find solutions stable across scenarios
* **Probabilistic Forecasting**: Quantify confidence in model predictions

**Validation and Calibration**

Rigorous validation ensures model accuracy:

* **Historical Validation**: Compare model results with observed data
* **Cross-Validation**: Test model performance across different regions
* **Sensitivity Testing**: Verify model response to parameter changes
* **Peer Review**: Open-source validation by research community

**Performance Metrics**

Comprehensive evaluation of model performance:

* **Economic Metrics**: Total system costs, investment requirements
* **Environmental Metrics**: Emissions, renewable energy shares
* **Technical Metrics**: System adequacy, grid utilization
* **Social Metrics**: Energy access, affordability indicators

For implementation details and code examples, see the :doc:`tutorial_electricity` and :doc:`tutorial_sector` sections.
