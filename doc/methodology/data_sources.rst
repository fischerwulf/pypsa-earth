.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _data_sources:

##########################################
Data Sources and Integration
##########################################

Overview
========

PyPSA-Earth's data infrastructure forms the foundation for accurate energy system modeling through systematic integration of diverse open-source datasets. This comprehensive data framework ensures reproducible, transparent, and scientifically rigorous modeling workflows that support reliable policy and investment decision-making.

**Data Integration Architecture:**

The data infrastructure operates through five interconnected layers:

1. **Raw Data Acquisition**: Automated collection from global repositories
2. **Quality Assurance**: Systematic validation and error detection
3. **Processing Pipeline**: Standardization and transformation workflows
4. **Integration Layer**: Cross-source validation and harmonization
5. **Model Interface**: Optimized data structures for energy modeling

**Core Data Categories:**

* **Geographic Data**: Infrastructure locations and network topology
* **Weather Data**: Renewable energy resources and climate patterns
* **Energy Statistics**: Demand patterns and generation profiles
* **Economic Data**: Technology costs and financial parameters
* **Policy Data**: Regulatory frameworks and emission targets

For detailed processing methodologies, see :doc:`data_processing`.

Geographic and Infrastructure Data
==================================

Overview
--------

Geographic and infrastructure data provide the spatial foundation for energy system modeling, defining network topology, administrative boundaries, and physical constraints. This data category encompasses infrastructure locations, transmission networks, and geographic features that influence energy system design and operation.

**Implementation Approach**:

Multiple data sources are combined to create comprehensive geographic representations of energy systems. Primary sources include crowd-sourced geographic databases, official government statistics, and regional utility databases. The integration process emphasizes data quality validation and spatial consistency across different sources.

Network Topology Data Sources
-----------------------------

**Primary Data Source: OpenStreetMap (OSM)**

OpenStreetMap provides the foundation for infrastructure mapping through crowd-sourced geographic data:

* **Infrastructure**: Substations, transmission lines, transformers, and generation facilities
* **Administrative Boundaries**: Countries, regions, and urban areas for spatial aggregation
* **Transportation Networks**: Roads, railways, and ports for logistics modeling
* **Natural Features**: Water bodies, protected areas, and terrain constraints

**Complementary Infrastructure Sources**

**World Bank Energy Database**
* **Coverage**: National energy statistics and infrastructure inventories
* **Validation Role**: Benchmark for network topology validation
* **Usage**: Gap-filling for regions with sparse OSM coverage
* **Update Frequency**: Annual releases with country-specific updates

**Global Power Plant Database**
* **Scope**: Comprehensive generation facility registry with location data
* **Integration**: Enhanced powerplantmatching for African coverage
* **Quality Control**: Automated duplicate detection and capacity reconciliation
* **Uncertainty Handling**: Confidence intervals for plant-level data

**Regional Transmission Organizations**
* **European Network of Transmission System Operators for Electricity (ENTSO-E)**: European transmission system data for validation
* **Southern African Power Pool (SAPP)**: Southern African Power Pool statistics
* **West African Power Pool (WAPP)**: West African Power Pool information
* **Integration**: Reference datasets for cross-validation

**Technical Details**

**Data Validation Procedures:**

1. **Completeness Assessment**: Systematic coverage analysis across study regions
2. **Accuracy Validation**: Cross-reference with satellite imagery and official utility data
3. **Consistency Verification**: Logical relationship checks between infrastructure elements
4. **Temporal Monitoring**: Regular updates to capture infrastructure evolution

**Quality Metrics and Acceptance Thresholds:**

* **Spatial Accuracy**: ±500m tolerance for transmission infrastructure
* **Attribute Completeness**: >80% coverage for critical infrastructure parameters
* **Temporal Freshness**: Monthly updates from OSM database
* **Cross-Validation**: >90% agreement with official utility data where available

**Missing Data Handling Strategies:**

1. **Hierarchical Fallback**: OpenStreetMap (OSM) → World Bank → Regional Organizations → Expert Estimates
2. **Interpolation Methods**: Spatial and temporal gap-filling algorithms
3. **Uncertainty Propagation**: Monte Carlo sampling for missing parameters
4. **Expert Validation**: Regional expert review for data-sparse areas

Weather and Climate Data
========================

Overview
--------

Weather and climate data provide the temporal and spatial characteristics of renewable energy resources, enabling accurate modeling of wind, solar, and hydro generation potential. This data category forms the foundation for renewable energy resource assessment and capacity factor calculations.

**Implementation Approach**:

Multiple meteorological data sources are integrated to create comprehensive weather datasets for renewable energy modeling. Primary sources include global reanalysis datasets and satellite-based observations. The processing pipeline converts raw meteorological data into technology-specific generation profiles while maintaining high temporal and spatial resolution.

Renewable Energy Resource Assessment
------------------------------------

**Primary Weather Data Sources**

**Fifth European Centre for Medium-Range Weather Forecasts (ECMWF) Reanalysis 5 (ERA5)**

Comprehensive weather dataset providing the foundation for renewable energy modeling:

* **Temporal Coverage**: 1979-present with hourly resolution
* **Spatial Resolution**: 0.25° × 0.25° grid (~25 km at equator)
* **Variables**: Wind speed, solar irradiance, temperature, precipitation
* **Quality Assurance**: Validated against global weather station networks

**Surface Solar Radiation Data Set - Heliosat (SARAH-2) Solar Radiation Database**

High-precision solar irradiance data for enhanced solar modeling:

* **Temporal Coverage**: 1983-present with 30-minute resolution
* **Spatial Resolution**: 0.05° × 0.05° grid (~5 km)
* **Geographic Focus**: Europe, Africa, and parts of South America
* **Validation**: Extensive ground station validation network

**Renewable Energy Conversion Models**

**Solar Photovoltaic (PV) Modeling:**
* **Irradiance Processing**: Horizontal to tilted plane conversion
* **Temperature Effects**: Cell temperature impact on efficiency
* **Technology Curves**: Different PV technologies (silicon, thin-film, etc.)
* **Soiling and Degradation**: Performance reduction factors

**Wind Energy Modeling:**
* **Wind Speed Extrapolation**: Hub height adjustment algorithms
* **Generation Curves**: Technology-specific wind-to-power conversion
* **Wake Effects**: Wind farm interaction modeling
* **Availability Factors**: Maintenance and grid curtailment

**Hydroelectric Power Modeling:**
* **Runoff Data**: River flow and reservoir level information
* **Seasonal Patterns**: Hydrological cycle capture
* **Environmental Constraints**: Ecological flow requirements
* **Cascade Effects**: Upstream-downstream interaction modeling

**Technical Details**

**Data Validation Procedures:**

1. **Bias Correction**: Systematic adjustment using ground observations
2. **Temporal Consistency**: Gap detection and anomaly identification
3. **Spatial Coherence**: Neighboring grid point correlation analysis
4. **Extreme Event Validation**: Comparison with historical weather records

**Quality Metrics and Acceptance Thresholds:**

* **Temporal Completeness**: >95% data availability for study periods
* **Spatial Coverage**: Global coverage with <0.25° resolution gaps
* **Accuracy Metrics**: 
  - Wind speed: ±15% mean absolute error
  - Solar irradiance: ±10% mean absolute error
  - Temperature: ±2°C mean absolute error

**Processing Pipeline Integration:**

1. **Data Acquisition**: Automated download from climate data servers
2. **Bias Correction**: Regional adjustment using ground observations
3. **Interpolation**: High-resolution grid generation from coarse data
4. **Capacity Factor Calculation**: Technology-specific conversion algorithms

**Uncertainty Quantification Methods:**

* **Ensemble Methods**: Multiple reanalysis product comparison
* **Confidence Intervals**: Statistical uncertainty estimation
* **Sensitivity Analysis**: Parameter uncertainty impact assessment
* **Scenario Testing**: Different weather year selections

Energy Statistics and Demand Data
=================================

Overview
--------

Energy statistics and demand data provide the foundation for understanding current energy consumption patterns and projecting future demand scenarios. This data category encompasses national energy balances, sectoral consumption profiles, and socio-economic drivers that influence energy demand across different regions and time periods.

**Implementation Approach**:

Multiple statistical databases and regional organizations provide complementary energy data that is integrated to create comprehensive demand profiles. The approach combines historical energy statistics with socio-economic indicators to generate spatially and temporally resolved demand projections. Machine learning techniques and statistical models are employed to handle data gaps and create robust demand forecasts.

National Energy Balances
------------------------

**Primary Statistical Sources**

**International Energy Agency (IEA)**

Comprehensive energy statistics forming the foundation for demand modeling:

* **World Energy Balances**: Annual energy flows by sector and fuel
* **World Energy Statistics**: Detailed supply and consumption data
* **Coverage**: Global with country-level detail
* **Temporal Range**: 1971-present with annual resolution

**United Nations (UN) Energy Statistics Database**

Complementary global energy data for validation and gap-filling:

* **Renewable Energy Statistics**: Detailed renewable capacity and generation
* **Accessibility**: Open access for developing country studies
* **Validation Role**: Cross-reference with IEA data for consistency
* **Integration**: Primary source for countries not covered by IEA

**Regional Energy Organizations**

Specialized regional data for enhanced accuracy:

* **European Network of Transmission System Operators for Electricity (ENTSO-E)**: European transmission system data with hourly resolution
* **Southern African Power Pool (SAPP)**: Southern African Power Pool statistics
* **West African Power Pool (WAPP)**: West African Power Pool information
* **Arab Union of Electricity**: Middle Eastern grid data

**Demand Modeling Methodology**

**Spatial Disaggregation Framework:**

1. **Population-Based**: Distribute demand using population density maps
2. **Economic Activity**: Gross Domestic Product (GDP) and industrial indicators for commercial/industrial load
3. **Urban-Rural Split**: Different consumption patterns by area type
4. **Sector-Specific**: Separate residential, commercial, and industrial demand

**Temporal Profiling System:**

* **Hourly Profiles**: Daily demand patterns by sector and season
* **Seasonal Variations**: Monthly and seasonal demand changes
* **Special Events**: Holiday and extreme weather adjustments
* **Load Duration Curves**: Statistical demand distributions

**Temperature-Dependent Demand Modeling:**

* **Heating Degree Days**: Space heating demand modeling
* **Cooling Degree Days**: Air conditioning demand patterns
* **Base Load**: Temperature-independent demand components
* **Saturation Effects**: Non-linear temperature relationships

**Technical Details**

**Data Validation Procedures:**

1. **Cross-Source Validation**: Comparison with UN Energy Statistics
2. **Temporal Consistency**: Trend analysis and anomaly identification
3. **Sectoral Balance**: Energy flow conservation checks
4. **Regional Coherence**: Neighboring country comparison

**Quality Metrics and Acceptance Thresholds:**

* **Data Completeness**: >90% coverage for key energy indicators
* **Temporal Consistency**: <15% year-over-year variation without explanation
* **Cross-Source Agreement**: <10% difference with alternative sources
* **Expert Validation**: Regional expert review for outlier detection

**Missing Data Handling Strategies:**

1. **Regression Models**: Predict missing values using available predictors
2. **Interpolation Methods**: Temporal and spatial gap-filling
3. **Proxy Indicators**: Alternative data sources for missing countries
4. **Expert Estimation**: Regional expert input for data-sparse areas

**Uncertainty Quantification Methods:**

* **Confidence Intervals**: Statistical uncertainty estimation for predictions
* **Sensitivity Analysis**: Parameter uncertainty impact assessment
* **Scenario Testing**: Different socio-economic pathway assumptions
* **Validation Metrics**: Out-of-sample prediction accuracy

Technology and Economic Data
============================

Overview
--------

Technology and economic data provide the cost parameters and performance characteristics necessary for energy system optimization and investment analysis. This data category encompasses technology costs, learning curves, economic projections, and regional cost variations that influence technology deployment decisions in energy system models.

**Implementation Approach**:

Multiple international organizations and research institutions provide technology cost databases that are integrated to create comprehensive economic parameter sets. The approach combines historical cost data with learning curve analysis to generate future cost projections. Regional cost variations and uncertainty quantification ensure robust economic modeling across different geographic contexts.

Technology Cost Data Sources
----------------------------

**Primary Cost Data Sources**

**International Renewable Energy Agency (IRENA)**

Primary source for renewable energy technology costs:

* **Renewable Power Generation Costs**: Annual technology cost updates
* **Global Energy Transformation**: Future cost projections
* **Regional Variations**: Cost differences by geographic region
* **Learning Curves**: Technology cost reduction trends

**International Energy Agency (IEA)**

Comprehensive technology analysis and projections:

* **Energy Technology Perspectives**: Detailed technology analysis
* **World Energy Outlook**: Long-term technology cost projections
* **Technology Roadmaps**: Specific technology cost and performance data
* **Scenario Development**: Multiple technology development pathways

**Danish Energy Agency (DEA)**

Detailed technical and economic parameters:

* **Technology Data**: Comprehensive technology database
* **Energy Storage**: Storage technology costs and performance
* **Sector Coupling**: Heat pumps, electrolyzers, and other technologies
* **Validation**: High-quality European technology data

**Cost Data Processing Pipeline**

1. **Currency Conversion**: Standardize to common currency (United States Dollar (USD) or Euro (EUR))
2. **Regional Adjustment**: Adapt costs for local economic conditions
3. **Temporal Alignment**: Ensure consistent reference years
4. **Uncertainty Quantification**: Provide cost ranges and confidence intervals

**Learning Curves and Projections**

**Historical Analysis Framework:**
* **Learning Rate Extraction**: Statistical analysis of historical cost data
* **Technology Clustering**: Group similar technologies for robust projections
* **Uncertainty Propagation**: Monte Carlo simulation of cost trajectories
* **Scenario Sensitivity**: Test different learning rate assumptions

**Future Projections Methodology:**
* **Deployment Scenarios**: Link cost reductions to deployment volumes
* **Technology Maturity**: Different learning rates by technology stage
* **Regional Variations**: Account for local manufacturing and markets
* **Validation**: Compare projections with recent cost developments

**Technical Details**

**Data Validation Procedures:**

1. **Multi-Source Comparison**: Cross-validate with International Energy Agency (IEA) and Danish Energy Agency (DEA) data
2. **Regional Consistency**: Verify geographic cost variations
3. **Temporal Trends**: Validate learning curve assumptions
4. **Technology Grouping**: Consistent categorization across sources

**Quality Metrics and Acceptance Thresholds:**

* **Source Agreement**: <20% difference between major sources
* **Temporal Consistency**: Logical cost evolution over time
* **Regional Plausibility**: Realistic cost variations by geography
* **Expert Validation**: Technology expert review of cost assumptions

Environmental and Policy Data
=============================

Overview
--------

Environmental and policy data provide the regulatory framework and emission constraints that guide energy system transitions and policy compliance. This data category encompasses climate policies, emission inventories, renewable energy targets, and carbon pricing mechanisms that influence energy system planning and operation.

**Implementation Approach**:

Climate policy databases and emission inventories from multiple international organizations are integrated to create comprehensive policy constraint sets. The approach combines quantitative emission data with qualitative policy frameworks to represent realistic regulatory environments. Regular updates ensure alignment with evolving climate policies and international agreements.

Emissions and Climate Data
--------------------------

**Primary Data Sources**

**Global Carbon Atlas**

Comprehensive emissions data for model validation:

* **Carbon Dioxide (CO2) Emissions**: National and regional emission inventories
* **Sectoral Breakdown**: Emissions by energy sector and fuel type
* **Temporal Coverage**: Annual data with historical trends
* **Validation**: Cross-reference with national inventories

**Climate Policy Databases**

* **Nationally Determined Contributions (NDCs)**: Country climate commitments
* **Renewable Energy Policies**: Support mechanisms and targets
* **Carbon Pricing**: Carbon tax and cap-and-trade systems
* **Energy Efficiency**: Standards and improvement targets

**Technical Details**

**Data Validation Procedures:**

1. **Policy Consistency**: Verify alignment between national policies and international commitments
2. **Temporal Tracking**: Monitor policy evolution and implementation progress
3. **Sectoral Analysis**: Assess policy impacts on different energy sectors
4. **Regional Coherence**: Compare policy frameworks across neighboring countries

**Quality Metrics and Acceptance Thresholds:**

* **Policy Coverage**: >90% of study regions have defined climate policies
* **Temporal Consistency**: Logical policy evolution over time
* **Quantitative Targets**: Measurable emission reduction and renewable energy targets
* **Expert Validation**: Climate policy expert review of policy interpretations

Data Integration and Validation Framework
=============================================

Overview
--------

The data integration and validation framework ensures consistent quality and reliability across all data sources used in PyPSA-Earth. This framework provides systematic procedures for data acquisition, validation, integration, and quality assurance that maintain scientific rigor and reproducibility throughout the modeling process.

**Implementation Approach**:

Automated data processing pipelines integrate multiple data sources while maintaining quality standards through continuous monitoring and validation procedures. The framework emphasizes reproducibility, version control, and uncertainty quantification to support transparent and reliable energy system modeling.

Automated Data Pipeline
-----------------------

**Continuous Data Quality Monitoring**

Systematic approach to maintain data quality throughout the modeling process:

1. **Real-Time Monitoring**: Automated alerts for data quality issues
2. **Version Control**: Track changes in input datasets and processing
3. **Quality Dashboards**: Visual monitoring of data quality metrics
4. **Automated Reports**: Regular data quality assessment reports

**Data Acquisition Workflow:**

1. **Automated Downloading**: Scheduled data updates from source Application Programming Interfaces (APIs)
2. **Format Standardization**: Convert to common data formats (Network Common Data Form (NetCDF), Comma-Separated Values (CSV), etc.)
3. **Quality Checks**: Automated validation and error detection
4. **Integration**: Combine multiple sources into model inputs
5. **Documentation**: Track data sources and processing steps

**Version Control and Reproducibility**

**Data Versioning System:**
* **Dataset Tracking**: Version control for all input datasets
* **Processing History**: Track all data transformation steps
* **Dependency Management**: Manage data source dependencies
* **Rollback Capability**: Ability to revert to previous data versions

**Reproducible Workflows:**
* **Automated Pipelines**: Fully automated data processing workflows
* **Documentation**: Comprehensive metadata for all data sources
* **Code Versioning**: Version-controlled data processing scripts
* **Environment Specification**: Reproducible computing environments

**Data Availability and Licensing**

**Open Data Commitment**

All data sources used in PyPSA-Earth are selected based on open access principles:

* **Open Source**: Freely available with permissive licenses
* **Academic Access**: Available for research purposes
* **Reproducible**: Processing methods fully documented
* **Citable**: Proper attribution to original data providers

**Licensing Framework:**
* **License Compatibility**: Ensure compatible licenses across all sources
* **Attribution Requirements**: Proper citation of all data sources
* **Usage Restrictions**: Respect any usage limitations
* **Redistribution Rights**: Clarify data redistribution permissions

**Data Sustainability:**
* **Long-term Availability**: Preference for stable, long-term data sources
* **Backup Strategies**: Multiple sources for critical data
* **Archive Policies**: Long-term data preservation strategies
* **Community Maintenance**: Community-driven data maintenance

**Technical Details**

**Validation Framework Components:**

**Cross-Source Validation:**
* **Consistency Checks**: Compare data from multiple sources
* **Outlier Detection**: Identify and flag anomalous data points
* **Trend Analysis**: Validate temporal patterns and relationships
* **Geographic Coherence**: Check spatial consistency of data

**Temporal Consistency:**
* **Trend Validation**: Check for logical time series patterns
* **Seasonality**: Verify expected seasonal patterns
* **Anomaly Detection**: Identify unusual temporal variations
* **Gap Analysis**: Assess temporal data completeness

**Spatial Consistency:**
* **Neighbor Correlation**: Check spatial correlations
* **Boundary Continuity**: Verify data consistency across boundaries
* **Resolution Consistency**: Ensure appropriate spatial resolution
* **Projection Accuracy**: Validate coordinate system transformations

**Expert Review Process:**
* **Regional Experts**: Subject matter expert validation of key datasets
* **Technical Review**: Methodology peer review
* **Stakeholder Feedback**: Input from energy sector professionals
* **Continuous Improvement**: Iterative refinement based on feedback

**Uncertainty Quantification Framework**

**Data Uncertainty Assessment:**
* **Source Uncertainty**: Quantify uncertainty in original data sources
* **Processing Uncertainty**: Assess uncertainty introduced by processing
* **Integration Uncertainty**: Uncertainty from combining multiple sources
* **Propagation Methods**: Monte Carlo and analytical uncertainty propagation

**Confidence Intervals:**
* **Statistical Methods**: Confidence interval estimation for all key parameters
* **Ensemble Approaches**: Multiple data source ensembles
* **Sensitivity Analysis**: Parameter uncertainty impact assessment
* **Scenario Testing**: Different data assumption scenarios

**Quality Assurance Metrics**

**Data Completeness Metrics:**
* **Spatial Coverage**: Percentage of study area with data
* **Temporal Coverage**: Percentage of study period with data
* **Attribute Completeness**: Percentage of required attributes present
* **Quality Scoring**: Composite data quality scores

**Accuracy Metrics:**
* **Validation Accuracy**: Comparison with ground truth data
* **Cross-Validation**: Out-of-sample prediction accuracy
* **Bias Assessment**: Systematic error identification
* **Uncertainty Bounds**: Confidence interval coverage

**Consistency Metrics:**
* **Inter-Source Agreement**: Agreement between different data sources
* **Temporal Consistency**: Logical temporal pattern adherence
* **Spatial Consistency**: Spatial pattern validation
* **Physical Consistency**: Adherence to physical constraints

Integration with Methodology Framework
======================================

**Cross-References to Methodology Sections:**

* :doc:`mathematical_framework` - Mathematical representation of data constraints
* :doc:`network_modeling` - Network topology data integration
* :doc:`data_processing` - Detailed processing methodologies
* :doc:`workflow_management` - Automated data pipeline management
* :doc:`validation_framework` - Data validation procedures and quality metrics

**Data-Methodology Integration:**

1. **Mathematical Constraints**: Data sources inform optimization constraints
2. **Network Construction**: Geographic data shapes network topology
3. **Processing Workflows**: Systematic data transformation pipelines
4. **Quality Assurance**: Integrated validation throughout modeling chain
5. **Uncertainty Handling**: Propagate data uncertainty through modeling

**Model Interface Design:**

* **Standardized Formats**: Common data formats for model inputs
* **Efficient Access**: Optimized data structures for model performance
* **Metadata Preservation**: Maintain data provenance throughout processing
* **Version Synchronization**: Coordinate data and model versions

References and Further Information
=================================

**Key Data Sources:**

* **OpenStreetMap**: https://www.openstreetmap.org/
Integration with Methodology Framework
======================================

**Cross-References to Methodology Sections:**

* :doc:`mathematical_framework` - Mathematical representation of data constraints
* :doc:`network_modeling` - Network topology data integration
* :doc:`data_processing` - Detailed processing methodologies
* :doc:`workflow_management` - Automated data pipeline management
* :doc:`validation_framework` - Data validation procedures and quality assurance

**External Data Sources:**

* **Fifth European Centre for Medium-Range Weather Forecasts (ECMWF) Reanalysis 5 (ERA5)**: https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels
* **International Energy Agency (IEA)**: https://www.iea.org/data-and-statistics
* **International Renewable Energy Agency (IRENA)**: https://www.irena.org/Data
* **World Bank Energy Data**: https://energydata.info/
* **OpenStreetMap (OSM)**: https://www.openstreetmap.org/
* **Global Carbon Atlas**: http://www.globalcarbonatlas.org/

**Related Documentation:**

* :doc:`data_processing` - Detailed processing methodologies
* :doc:`validation_framework` - Data validation procedures
* :doc:`workflow_management` - Automated data pipelines
* :doc:`../tutorial_electricity` - Data usage examples
* :doc:`../populate_data` - Data population workflows

**Technical Standards:**

* **International Organization for Standardization (ISO) 19115**: Geographic information metadata standards
* **Climate and Forecast (CF) Conventions**: Climate and forecast metadata conventions
* **Findable, Accessible, Interoperable, Reusable (FAIR) Principles**: Findable, Accessible, Interoperable, Reusable data
* **Open Data Charter**: International open data principles
