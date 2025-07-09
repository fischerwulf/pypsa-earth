.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _validation_framework:

##########################################
Validation Framework
##########################################

Overview
========

PyPSA-Earth employs comprehensive validation approaches to ensure model accuracy, reliability, and performance across different scales and regions. This systematic validation framework addresses five critical areas: network topology validation, electricity consumption validation, renewable resource validation, power plant fleet validation, and operational validation.

The validation methodology integrates multiple data sources and benchmarks to verify model outputs against real-world observations. This ensures that PyPSA-Earth maintains high standards for energy system modeling and provides reliable results for policy and investment decision-making.

Network Topology Validation
============================

OpenStreetMap Data Validation
-----------------------------

**Validation Methodology**

Network topology validation compares PyPSA-Earth's OpenStreetMap-based network construction with official transmission system operator data and World Bank datasets. This multi-source comparison ensures network accuracy across different geographic scales.

**Circuit Length Validation**

Transmission line validation focuses on total circuit lengths at different AC voltage levels. Circuit lengths multiply line distances by the number of circuits, providing a comprehensive measure of transmission capacity:

* **110-220 kV circuits**: Regional distribution networks
* **220-380 kV circuits**: National transmission backbones  
* **>380 kV circuits**: International interconnections

**Regional Performance Analysis**

For Nigeria, the validation shows:

* World Bank data aligns with official transmission company statistics
* PyPSA-Earth's cleaned OpenStreetMap data provides 35% shorter circuit lengths than official data
* Continental scale: OpenStreetMap provides 117% longer circuit lengths than World Bank data

**Quality Assurance Procedures**

1. **Multi-source comparison**: Cross-validate against World Bank, national utility data, and OpenStreetMap
2. **Topological verification**: Visual comparison of network structures across data sources
3. **Statistical validation**: Circuit length comparisons at different voltage levels
4. **Continuous monitoring**: Regular updates as OpenStreetMap data evolves

Electricity Consumption Validation
==================================

Demand Prediction Validation
----------------------------

**Validation Framework**

Electricity consumption validation compares PyPSA-Earth's demand predictions with Our World in Data and national statistics. The validation covers temporal patterns, magnitude accuracy, and regional distribution.

**GEGIS Performance Metrics**

The Global Energy GIS (GEGIS) demand prediction system shows:

* **Overall accuracy**: 8% absolute error across 44 countries
* **Performance variation**: Better performance in high-income countries
* **Temporal validation**: Hourly pattern verification against historical data
* **Spatial validation**: Regional demand distribution accuracy

**Error Analysis and Acceptance Criteria**

* **Acceptable error threshold**: ±15% for national annual consumption
* **Temporal accuracy**: ±20% for daily and seasonal patterns
* **Regional accuracy**: ±25% for subnational demand distribution
* **Performance degradation**: Lower accuracy in low-income countries acknowledged

**Continuous Validation Procedures**

1. **Annual recalibration**: Update against latest consumption statistics
2. **Cross-validation**: Compare predictions with multiple data sources
3. **Uncertainty quantification**: Estimate confidence intervals for predictions
4. **Performance monitoring**: Track prediction accuracy over time

Renewable Resource Validation
=============================

Solar and Wind Potential Validation
-----------------------------------

**Validation Methodology**

Renewable resource validation compares PyPSA-Earth's technical potential estimates with international organization reports, particularly IRENA and Global Wind Energy Council assessments.

**Technical Potential Comparison**

**Wind Energy Validation:**
* IRENA/GWEC estimate: 180,000 TWh for Africa
* PyPSA-Earth estimate: 108,700 TWh for Africa
* Validation metric: Sufficient to electrify continent 250 times vs. 150 times

**Solar Energy Validation:**
* IRENA estimate: 660,000 TWh for Africa  
* PyPSA-Earth estimate: 122,200 TWh for Africa
* Validation metric: Sufficient to electrify continent 916 times vs. 169 times

**Power Density Validation**

The technical potential differences stem from:

* **Excluded areas**: Conservative land-use constraints in PyPSA-Earth
* **Power density factors**: 46.4 MW/km² for solar PV (conservative approach)
* **Land allocation**: Realistic constraints vs. theoretical maximum potential
* **Social-technical considerations**: Practical deployment limitations

**Capacity Factor Validation**

1. **Temporal validation**: Compare hourly generation patterns with satellite data
2. **Spatial validation**: Regional capacity factor variations
3. **Seasonal validation**: Monthly and seasonal generation patterns
4. **Technology validation**: Different renewable technology performance

Power Plant Fleet Validation
============================

Installed Capacity Validation
-----------------------------

**Validation Approach**

Power plant database validation compares PyPSA-Earth's site-specific power plant database with national statistics from IRENA and USAID. This validation ensures accurate representation of existing generation capacity.

**Capacity Matching Performance**

**Overall Accuracy:**
* PyPSA-Earth matches 165 GW out of 229 GW reported by IRENA (72% accuracy)
* Most technologies show 2-15% error rates
* Larger differences for coal and gas plants due to recent installations

**Technology-Specific Validation:**

* **Hydro**: High accuracy (±5% typical error)
* **Solar**: Excellent accuracy (±2% typical error)
* **Wind**: Good accuracy (±10% typical error)
* **Coal/Gas**: Moderate accuracy (±15% typical error)
* **Missing technologies**: Geothermal and CSP not yet included

**Data Quality Improvements**

1. **Powerplantmatching enhancement**: Extended database for African coverage
2. **OpenStreetMap integration**: Additional power plant location data
3. **Duplicate detection**: Automated removal of redundant entries
4. **Capacity reconciliation**: Cross-validation between multiple sources

**Limitations and Future Improvements**

* Recent installation data gaps (3-4 year lag)
* Need for more frequent database updates
* Technology coverage expansion (geothermal, CSP)
* Enhanced validation for distributed generation

Operational Validation
======================

Dispatch Validation Methodology
-------------------------------

**Nigeria 2020 Case Study**

Operational validation demonstrates PyPSA-Earth's optimization capabilities through dispatch validation using Nigeria's 2020 power system as a benchmark.

**Validation Setup**

* **Network**: 54-node clustered representation of Nigeria
* **Demand**: 29.5 TWh total (vs. 28.2 TWh Our World in Data)
* **Optimization**: Dispatch optimization with linear optimal power flow
* **Validation metric**: Generation mix comparison

**Generation Mix Validation Results**

==================  ============  ================  =======
Technology          PyPSA-Earth   Our World Data    Error
==================  ============  ================  =======
Solar               0.04 TWh      0.04 TWh         0%
Wind                0 TWh         0 TWh            0%
Hydro               5.8 TWh       6.1 TWh          -5%
Gas                 23.6 TWh      21.4 TWh         +10%
Coal                0 TWh         0.6 TWh          -100%
==================  ============  ================  =======

**Validation Analysis**

* **Overall accuracy**: Excellent representation of generation mix
* **Solar validation**: Perfect match (100% accuracy)
* **Gas generation**: 2 TWh (10%) higher than benchmark
* **Hydro generation**: 0.3 TWh (5%) lower than benchmark
* **Marginal cost validation**: 59 €/MWh (vs. 45-70 €/MWh reported range)

**Dispatch Pattern Validation**

1. **Temporal validation**: Hourly dispatch patterns match expected behavior
2. **Economic validation**: Merit order dispatch follows cost assumptions
3. **Constraint validation**: Power flow limits properly enforced
4. **Reliability validation**: System adequacy maintained

Computational Performance Validation
====================================

Scalability Assessment
---------------------

**Performance Benchmarks**

PyPSA-Earth's computational performance has been validated across different spatial resolutions and solver configurations for the Nigeria 2020 case study.

**Solver Performance Comparison**

**Gurobi 9.5.1 (Commercial):**
* **4 threads**: Highly efficient, sub-hour solution times
* **Memory usage**: Optimized for large-scale problems
* **Convergence**: Reliable convergence across all problem sizes

**HiGHS 1.2.1 (Open-source):**
* **Single core**: Competitive performance with commercial solvers
* **Solution time**: Under one day for full Nigeria model
* **Memory requirements**: Laptop-compatible resource usage

**CBC 2.10.8 (Open-source):**
* **Single core**: Slower but reliable performance
* **Resource usage**: Higher memory requirements than HiGHS
* **Scalability**: Limited parallel processing capabilities

**Scalability Metrics**

* **Problem size**: 4 to 54 nodes tested
* **Memory scaling**: Linear relationship with problem size
* **Solution time**: Polynomial scaling with network complexity
* **Parallel efficiency**: Good scaling with available cores (Gurobi)

**Performance Optimization Strategies**

1. **Network clustering**: Reduce problem size while preserving essential characteristics
2. **Temporal aggregation**: Representative time periods for long-term studies
3. **Solver selection**: Choose appropriate solver based on problem characteristics
4. **Memory management**: Efficient data structures and garbage collection

Quality Assurance Framework
===========================

Continuous Validation Workflows
-------------------------------

**Automated Quality Assurance**

PyPSA-Earth implements automated validation workflows that continuously monitor model accuracy and performance across all validation dimensions.

**Data Quality Monitoring**

1. **Input validation**: Automated checks for data completeness and consistency
2. **Output validation**: Statistical tests against historical benchmarks
3. **Performance monitoring**: Tracking solution quality and computational efficiency
4. **Error detection**: Automated identification of anomalous results

**Validation Workflow Integration**

* **Pre-processing validation**: Data quality checks before model runs
* **Runtime validation**: Solution feasibility and convergence monitoring
* **Post-processing validation**: Output verification against benchmarks
* **Continuous integration**: Automated validation in development workflow

**Error Handling and Reporting**

1. **Error classification**: Categorize validation failures by severity
2. **Automated reporting**: Generate validation reports for each model run
3. **Threshold monitoring**: Alert when validation metrics exceed acceptable limits
4. **Version control**: Track validation performance across model versions

**Regional Adaptation Strategies**

Different regions require specific validation approaches:

* **Data-rich regions**: Comprehensive multi-source validation
* **Data-sparse regions**: Conservative assumptions and uncertainty quantification
* **Developing regions**: Focus on capacity building and data collection
* **Island systems**: Specialized validation for isolated grid systems

Future Validation Enhancements
==============================

Planned Improvements
-------------------

**Enhanced Network Validation**

* **Image recognition**: Automated extraction of transmission data from satellite imagery
* **Real-time validation**: Integration with live grid monitoring systems
* **Topology evolution**: Dynamic validation as network infrastructure changes
* **Cross-border validation**: International interconnection accuracy

**Advanced Demand Validation**

* **Machine learning enhancement**: Improved prediction algorithms for developing regions
* **High-frequency validation**: Sub-hourly demand pattern validation
* **Sector-specific validation**: Industrial, residential, and commercial demand patterns
* **Climate impact validation**: Temperature-dependent demand correlation

**Renewable Resource Enhancement**

* **Satellite validation**: Direct comparison with satellite-based resource assessment
* **Meteorological validation**: Integration with weather station data
* **Technological validation**: Advanced turbine and panel performance models
* **Grid integration validation**: Transmission constraint impact on potential

**Operational Validation Expansion**

* **Multi-country validation**: Extended dispatch validation across regions
* **Sector coupling validation**: Integrated energy system validation
* **Flexibility validation**: Storage and demand response performance
* **Reliability validation**: System adequacy and resilience metrics

References
==========

For related information, see:

* :doc:`mathematical_framework` - Optimization formulations and solution properties
* :doc:`network_modeling` - Network construction and topology validation
* :doc:`data_processing` - Data validation procedures and quality assurance
* :doc:`workflow_management` - Automated validation workflows and quality control
* :doc:`../data_sources` - Data sources and validation benchmarks
* :doc:`../tutorial_electricity` - Validation examples and case studies
* :doc:`../capabilities` - Model applications and performance demonstrations

**Key Validation Publications:**

* Parzen, M. et al. (2023). "PyPSA-Earth. A new global open energy system optimization model demonstrated in Africa." *Applied Energy* 341, 121096.
* International Renewable Energy Agency (IRENA). Various renewable energy statistics and technical potential assessments.
* Our World in Data. Energy consumption and generation statistics for validation benchmarks.
* Global Wind Energy Council (GWEC). Wind energy technical potential assessments.

**Validation Data Sources:**

* **Network Topology**: OpenStreetMap, World Bank transmission data, national utility statistics
* **Electricity Consumption**: Our World in Data, national statistics, GEGIS validation dataset
* **Renewable Resources**: IRENA technical potential, GWEC wind assessments, satellite data
* **Power Plant Fleet**: IRENA capacity statistics, USAID data, powerplantmatching database
* **Operational Validation**: National dispatch statistics, transmission system operator data
