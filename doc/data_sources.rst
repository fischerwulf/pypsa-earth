.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _data_sources:

##########################################
Data Sources and Processing
##########################################

Overview
========

PyPSA-Earth leverages a comprehensive suite of open-source data to create accurate energy system models. The framework's strength lies in its ability to automatically process and integrate diverse data sources, ensuring reproducible and transparent modeling workflows.

**Data Categories:**

* **Geographic Data**: Infrastructure locations and network topology
* **Weather Data**: Renewable energy resources and climate patterns
* **Energy Statistics**: Demand patterns and generation profiles
* **Economic Data**: Technology costs and financial parameters
* **Policy Data**: Regulatory frameworks and emission targets

Geographic and Infrastructure Data
==================================

**OpenStreetMap (OSM)**

Primary source for infrastructure mapping:

* **Power Infrastructure**: Substations, transmission lines, and power plants
* **Transportation Networks**: Roads, railways, and ports for logistics modeling
* **Administrative Boundaries**: Countries, regions, and urban areas
* **Natural Features**: Water bodies, protected areas, and terrain data

**Processing Methodology:**

1. **Automated Extraction**: Query OSM databases using Overpass API
2. **Data Cleaning**: Remove incomplete or inconsistent records
3. **Validation**: Cross-reference with external databases
4. **Standardization**: Convert to consistent coordinate systems and units

**Data Quality Assurance:**

* **Completeness Checks**: Verify coverage across study regions
* **Accuracy Validation**: Compare with satellite imagery and field data
* **Consistency Analysis**: Ensure logical relationships between infrastructure elements
* **Temporal Updates**: Regular data refreshes to capture infrastructure changes

**Global Energy Infrastructure Database**

Complementary infrastructure data sources:

* **World Bank Energy Database**: National energy statistics and infrastructure
* **IRENA Global Energy Atlas**: Renewable energy potential and projects
* **Global Power Plant Database**: Comprehensive power plant registry
* **Regional Transmission Organizations**: Detailed grid data where available

Weather and Climate Data
========================

**Renewable Energy Resource Assessment**

Multiple weather datasets for comprehensive resource evaluation:

**ERA5 Reanalysis Data (Primary Source)**

* **Temporal Coverage**: 1979-present with hourly resolution
* **Spatial Resolution**: 0.25° × 0.25° grid (~25 km)
* **Variables**: Wind speed, solar irradiance, temperature, precipitation
* **Quality**: Validated against global weather station networks

**SARAH Solar Radiation Database**

* **Temporal Coverage**: 1983-present with 30-minute resolution
* **Spatial Resolution**: 0.05° × 0.05° grid (~5 km)
* **Focus**: High-precision solar irradiance data
* **Coverage**: Europe, Africa, and parts of South America

**MERRA-2 Reanalysis**

* **Temporal Coverage**: 1980-present with hourly resolution
* **Spatial Resolution**: 0.5° × 0.625° grid (~50 km)
* **Strengths**: Aerosol data for solar resource assessment
* **Usage**: Validation and gap-filling for ERA5 data

**Processing Pipeline:**

1. **Data Acquisition**: Automated download from climate data servers
2. **Bias Correction**: Adjust for systematic errors using ground observations
3. **Interpolation**: Generate high-resolution grids from coarse data
4. **Capacity Factor Calculation**: Convert weather data to technology-specific outputs

**Renewable Energy Conversion Models**

**Solar Photovoltaic:**

* **Irradiance Processing**: Convert from horizontal to tilted plane irradiance
* **Temperature Effects**: Account for cell temperature on efficiency
* **Technology Curves**: Different PV technologies (silicon, thin-film, etc.)
* **Soiling and Degradation**: Include performance reduction factors

**Wind Energy:**

* **Wind Speed Extrapolation**: Adjust to turbine hub heights
* **Power Curves**: Technology-specific wind-to-power conversion
* **Wake Effects**: Model wind farm interactions
* **Availability Factors**: Include maintenance and grid curtailment

**Hydroelectric Power:**

* **Runoff Data**: River flow and reservoir level information
* **Seasonal Patterns**: Capture hydrological cycles
* **Environmental Constraints**: Include ecological flow requirements
* **Cascade Effects**: Model upstream-downstream interactions

Energy Statistics and Demand Data
=================================

**National Energy Balances**

Comprehensive energy statistics from multiple sources:

**International Energy Agency (IEA)**

* **World Energy Balances**: Annual energy flows by sector and fuel
* **World Energy Statistics**: Detailed supply and consumption data
* **Coverage**: Global with country-level detail
* **Temporal Range**: 1971-present with annual resolution

**UN Energy Statistics**

* **Energy Statistics Database**: Comprehensive global energy data
* **Renewable Energy Statistics**: Detailed renewable capacity and generation
* **Validation**: Cross-reference with IEA data for consistency
* **Accessibility**: Open access for developing country studies

**Regional Energy Organizations**

* **ENTSO-E**: European transmission system data
* **SAPP**: Southern African Power Pool statistics
* **WAPP**: West African Power Pool information
* **Arab Union of Electricity**: Middle Eastern grid data

**Demand Modeling Methodology**

**Spatial Disaggregation:**

1. **Population-Based**: Distribute demand using population density
2. **Economic Activity**: Use GDP and industrial indicators
3. **Urban-Rural Split**: Different consumption patterns by area type
4. **Sector-Specific**: Separate residential, commercial, and industrial demand

**Temporal Profiling:**

* **Hourly Profiles**: Daily demand patterns by sector
* **Seasonal Variations**: Monthly and seasonal demand changes
* **Special Events**: Holiday and extreme weather adjustments
* **Load Duration Curves**: Statistical demand distributions

**Temperature-Dependent Demand:**

* **Heating Degree Days**: Space heating demand modeling
* **Cooling Degree Days**: Air conditioning demand patterns
* **Base Load**: Temperature-independent demand components
* **Saturation Effects**: Non-linear temperature relationships

Technology and Economic Data
============================

**Technology Cost Data**

Multiple sources for comprehensive cost coverage:

**International Renewable Energy Agency (IRENA)**

* **Renewable Power Generation Costs**: Annual technology cost updates
* **Global Energy Transformation**: Future cost projections
* **Regional Variations**: Cost differences by geographic region
* **Learning Curves**: Technology cost reduction trends

**International Energy Agency (IEA)**

* **Energy Technology Perspectives**: Comprehensive technology analysis
* **World Energy Outlook**: Long-term technology cost projections
* **Technology Roadmaps**: Detailed cost and performance data
* **Projected Costs**: Future technology cost scenarios

**Danish Energy Agency (DEA)**

* **Technology Data**: Detailed technical and economic parameters
* **Energy Storage**: Comprehensive storage technology database
* **Sector Coupling**: Heat pumps, electrolyzers, and other technologies
* **Validation**: Cross-reference with other international sources

**Cost Data Processing:**

1. **Currency Conversion**: Standardize to common currency (USD or EUR)
2. **Regional Adjustment**: Adapt costs for local economic conditions
3. **Temporal Alignment**: Ensure consistent reference years
4. **Uncertainty Quantification**: Provide cost ranges and confidence intervals

**Learning Curves and Projections**

* **Historical Analysis**: Extract learning rates from historical data
* **Future Projections**: Apply learning curves to future deployments
* **Scenario Sensitivity**: Test different learning rate assumptions
* **Technology Clusters**: Group similar technologies for robust projections

Environmental and Policy Data
=============================

**Emissions Data**

**Global Carbon Atlas**

* **CO2 Emissions**: National and regional emission inventories
* **Sectoral Breakdown**: Emissions by energy sector
* **Temporal Coverage**: Annual data with historical trends
* **Validation**: Cross-reference with national inventories

**Climate Policy Databases**

* **Nationally Determined Contributions (NDCs)**: Country climate commitments
* **Renewable Energy Policies**: Support mechanisms and targets
* **Carbon Pricing**: Carbon tax and cap-and-trade systems
* **Energy Efficiency**: Standards and improvement targets

**Data Integration and Validation**
==================================

**Automated Data Pipeline**

Streamlined processing for reproducible results:

1. **Data Acquisition**: Automated downloading and updating
2. **Format Standardization**: Convert to common data formats
3. **Quality Checks**: Automated validation and error detection
4. **Integration**: Combine multiple sources into model inputs
5. **Documentation**: Track data sources and processing steps

**Validation Framework**

* **Cross-Source Validation**: Compare data from multiple sources
* **Temporal Consistency**: Check for logical time series patterns
* **Spatial Consistency**: Verify geographic data coherence
* **Expert Review**: Subject matter expert validation of key datasets

**Version Control and Reproducibility**

* **Data Versioning**: Track changes in input datasets
* **Processing Scripts**: Version-controlled data processing code
* **Documentation**: Comprehensive metadata for all data sources
* **Reproducible Workflows**: Automated pipeline for data updates

**Data Availability and Licensing**

All data sources used in PyPSA-Earth are either:

* **Open Source**: Freely available with permissive licenses
* **Academic Access**: Available for research purposes
* **Reproducible**: Processing methods fully documented
* **Citable**: Proper attribution to original data providers

For detailed implementation examples, see the :doc:`tutorial_electricity` and :doc:`populate_data` sections.
