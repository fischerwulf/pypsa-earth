.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _network_modeling:

##########################################
Network Modeling
##########################################

Overview
========

PyPSA-Earth's network modeling combines automated data processing with sophisticated algorithms to create realistic representations of power systems worldwide. The approach addresses the fundamental challenge of limited open power grid data availability, particularly in developing regions, by reconstructing network topology from globally available open-source geospatial datasets.

The network modeling methodology encompasses three core components:

1. **OpenStreetMap-based network construction** - Automated extraction and processing of transmission infrastructure data
2. **Fundamental shapes methodology** - Spatial data aggregation strategies for model efficiency
3. **Network optimization techniques** - Clustering and augmentation methods for computational tractability

This comprehensive approach enables PyPSA-Earth to model energy systems at any scale while maintaining high spatial resolution and computational efficiency.

OpenStreetMap Data Extraction Methodology
=========================================

Network Data Challenges
-----------------------

The most comprehensive and accurate data on power grids are typically curated by transmission system operators. However, the availability of open power grid data remains relatively low for many parts of the world, with particularly sparse coverage in Africa and other developing regions.

Existing open-source packages (e.g., Gridkit, Transnet, SciGrid) focus on specific regional applications rather than providing global coverage. To address this limitation, PyPSA-Earth has developed an original approach that reconstructs network topology using solely open, globally-available data.

OpenStreetMap Foundation
-----------------------

The methodology is based on OpenStreetMap (OSM) datasets, which provide:

* **Crowd-sourced geographic information** - Daily updated global infrastructure data
* **Comprehensive coverage** - Geolocation data for power system components worldwide
* **Open accessibility** - Freely available under open licenses
* **Community validation** - Continuous improvement through collaborative editing

**Methodological Rationale**

The choice of OSM as the primary data source reflects a strategic decision to prioritize:

1. **Global consistency** - Unlike proprietary datasets that may have regional gaps or inconsistent coverage, OSM provides a unified data structure worldwide
2. **Temporal currency** - Daily updates ensure the network topology reflects recent infrastructure developments, critical for rapidly changing power systems
3. **Reproducibility** - Open licensing enables transparent research and allows other researchers to validate and extend the methodology
4. **Community-driven quality** - The collaborative nature of OSM means errors are typically identified and corrected by the global community more rapidly than in static datasets

Three-Step Network Topology Creation Process
============================================

The electricity network topology is created through three novel steps that transform raw OSM data into model-ready network representations:

Step 1: Data Downloading
-----------------------

**esy-osm Tool Integration**

PyPSA-Earth employs the esy-osm tool for efficient OSM data retrieval:

* **Multi-threaded processing** - Parallel download capabilities for large geographic areas
* **Selective feature extraction** - Targeted retrieval of power system components
* **Optimized data handling** - Memory-efficient processing of large datasets

**Component Identification**

The download process targets specific OSM features representing:

* **Substations** - High-voltage switching and transformation facilities
* **Transformers** - Voltage level conversion equipment  
* **Power lines** - Transmission and sub-transmission circuits
* **Converters** - AC/DC conversion facilities

Step 2: Filtering and Cleaning
-----------------------------

**Data Structure Alignment**

Raw OSM data undergoes comprehensive cleaning to ensure compatibility with PyPSA framework requirements:

* **Geospatial description standardization** - Consistent coordinate systems and projections
* **Component classification** - Voltage level categorization and technology identification
* **Data validation** - Quality checks for completeness and consistency
* **Topology verification** - Connection validation and error correction

**Quality Improvement Approaches**

Advanced algorithms improve the quality of OSM-extracted grid topology:

* **Coordinate tolerance management** - Accounting for GPS accuracy limitations in OSM data
* **Spatial clustering** - Grouping nearby components representing the same infrastructure
* **Connectivity analysis** - Ensuring realistic network connectivity patterns
* **Error detection and correction** - Automated identification and resolution of data inconsistencies

**Rationale for Quality Enhancement**

The quality improvement approach addresses inherent limitations in crowd-sourced data:

- **GPS precision variability** - Different contributors use devices with varying accuracy, requiring tolerance algorithms that can identify when multiple OSM entries represent the same physical infrastructure
- **Incomplete connectivity information** - OSM may contain substations and power lines as separate entities without explicit connectivity relationships, necessitating spatial analysis to infer logical connections
- **Temporal inconsistencies** - Infrastructure changes over time, and quality algorithms help identify and resolve conflicting information from different time periods

Step 3: Building Meshed Network Datasets
----------------------------------------

**Component Integration**

The final step constructs complete network datasets incorporating:

* **HVAC components** - High voltage alternating current transmission lines and equipment
* **HVDC components** - High voltage direct current links for long-distance transmission
* **Multi-voltage integration** - Representation of transmission, sub-transmission, and distribution levels
* **Interconnection modeling** - Cross-border and inter-regional connections

**Network Mesh Construction**

Advanced algorithms create realistic network topologies:

* **Automatic connection inference** - Logical connections between nearby components
* **Voltage level consistency** - Appropriate connections within and between voltage levels
* **Geographic constraints** - Consideration of terrain and infrastructure limitations
* **Redundancy representation** - Multiple transmission paths for reliability modeling

Fundamental Shapes Methodology
==============================

Fundamental shapes represent the smallest defined regions that gather various data types to characterize the energy system. These shapes serve as the spatial foundation for data aggregation and model execution, providing the geometric basis for integrating diverse datasets into a coherent modeling framework.

Before model execution, energy system data is typically provided in various formats (geo-referenced point locations, raster data, administrative boundaries). The fundamental shapes methodology ensures proper aggregation and spatial consistency across all data sources.

Onshore Region Modeling
-----------------------

**Administrative Zones Approach**

PyPSA-Earth provides two primary methods for creating onshore fundamental shapes:

1. **Global Administrative Areas (GADM)** - Retrieval of administrative zones at various hierarchical levels:
   
   * **National level** - Country-wide administrative boundaries
   * **Regional level** - State or provincial boundaries  
   * **Municipal level** - Local administrative units
   
   This approach facilitates clear communication of results to policymakers and stakeholders by aligning with existing administrative structures.

2. **Voronoi Partitioned Areas** - Spatial tessellation based on substation locations:
   
   * **Centroid-based construction** - Uses substation GIS coordinates as seed points
   * **Equidistant boundaries** - Each boundary point is equidistant from nearest substation centroids
   * **Network-accurate representation** - Reflects actual electrical network topology

**Configuration Decision Framework**

The choice between GADM and Voronoi approaches depends on the study objectives:

**GADM Administrative Zones - Optimal for:**
- **Policy analysis studies** - Results align with jurisdictional boundaries for regulatory decision-making
- **National energy planning** - Facilitates coordination between different administrative levels
- **Stakeholder communication** - Familiar boundaries improve understanding and acceptance of results
- **Data integration** - Many socio-economic datasets are organized by administrative boundaries

**Voronoi Partitioned Areas - Optimal for:**
- **Technical system studies** - Better represents actual electrical service areas and load flow patterns
- **Infrastructure planning** - Reflects real electrical connectivity and transmission constraints
- **Operational analysis** - Accurately captures electrical distance and system behavior
- **High-resolution modeling** - Provides finer spatial granularity for detailed technical analysis

**Hybrid Approaches** - Some studies benefit from combining both methods, using GADM for result presentation and Voronoi for technical calculations.

**Spatial Data Integration**

The fundamental shapes approach enables:

* **Multi-source data aggregation** - Consistent spatial framework for diverse datasets
* **Resolution flexibility** - Scalable from high-resolution local studies to continental analysis
* **Topological consistency** - Maintains electrical network connectivity relationships

Offshore Region Modeling
------------------------

**Exclusive Economic Zones Integration**

For offshore regions, PyPSA-Earth employs a specialized approach:

* **Voronoi-based methodology** - Uses high-voltage onshore nodes as seed points
* **Maritime boundary constraints** - Limited by Exclusive Economic Zones (EEZ) data for each country
* **Offshore resource integration** - Enables modeling of offshore wind and other marine resources

**Offshore Methodology Rationale**

The offshore approach addresses unique challenges in marine energy system modeling:

- **Electrical connectivity projection** - Offshore resources must connect to onshore networks, making onshore substations the natural basis for offshore zone definition
- **Jurisdictional constraints** - EEZ boundaries ensure compliance with international maritime law and resource ownership rights
- **Resource accessibility** - Voronoi tessellation from onshore nodes naturally reflects the economic feasibility of offshore development based on transmission distance
- **Cross-border coordination** - EEZ integration enables modeling of international offshore grid connections while respecting territorial boundaries

**Usage Scenarios:**
- **Offshore wind planning** - Optimal for identifying development zones and grid connection strategies
- **Marine spatial planning** - Integrates electrical infrastructure needs with other maritime uses
- **International cooperation studies** - Facilitates modeling of cross-border offshore transmission projects

**Spatial Extent Definition**

The offshore fundamental shapes methodology:

* **Extends onshore network influence** - Projects electrical connectivity into maritime areas
* **Respects international boundaries** - Adheres to established maritime territorial limits
* **Enables cross-border modeling** - Supports international offshore interconnections

Network Simplification Strategies
=================================

PyPSA-Earth implements state-of-the-art spatial clustering methods to address the computational complexity of co-optimization problems involving transmission and generation capacity expansion.

Clustering Algorithms
--------------------

**Hierarchical Clustering Methods**

The model offers four distinct clustering approaches:

1. **Variable Potential Clustering**
   
   * **Renewable resource focus** - Conserves representation of solar and wind potentials
   * **Demand pattern preservation** - Maintains electricity demand characteristics
   * **Hierarchical approach** - Inspired by established clustering methodologies
   * **Physical connectivity constraint** - Only aggregates nodes connected by physical transmission lines

2. **Transmission Grid Clustering**
   
   * **Impedance-based methodology** - Density-based hierarchical clustering on line impedance
   * **Electrical parameter accuracy** - Improves power flow estimates in aggregated models
   * **Grid topology focus** - Maintains essential transmission network characteristics

3. **Spatial Proximity Clustering**
   
   * **Weighted k-means algorithm** - Operates on geographic coordinates of network nodes
   * **Distance-based aggregation** - Groups spatially proximate nodes
   * **Computational efficiency** - Reduces model complexity while maintaining spatial relationships

4. **Administrative Boundary Clustering**
   
   * **GADM shapes integration** - Aggregates nodes within administrative boundaries
   * **Policy relevance** - Facilitates results interpretation for policy recommendations
   * **Institutional alignment** - Supports decision-making frameworks

**Clustering Method Selection Strategy**

The choice of clustering method depends on the specific modeling objectives and computational constraints:

**Variable Potential Clustering - Recommended for:**
- **Renewable integration studies** - Preserves spatial diversity of renewable resources critical for variability analysis
- **Resource assessment** - Maintains representation of location-specific capacity factors and generation profiles
- **Long-term planning** - Ensures optimal renewable resource allocation in capacity expansion studies

**Transmission Grid Clustering - Recommended for:**
- **Grid stability analysis** - Maintains electrical characteristics essential for power flow accuracy
- **Transmission planning** - Preserves impedance relationships critical for line loading and voltage analysis
- **Operational studies** - Retains electrical distance metrics important for system operation

**Spatial Proximity Clustering - Recommended for:**
- **Computational efficiency priority** - Fastest clustering method for large-scale studies
- **Geographic analysis** - Maintains spatial relationships for visualization and geographic interpretation
- **First-approximation studies** - Suitable for preliminary analysis when detailed electrical characteristics are less critical

**Administrative Boundary Clustering - Recommended for:**
- **Policy analysis** - Results aligned with jurisdictional boundaries for regulatory decision-making
- **National energy planning** - Facilitates coordination between different governmental levels
- **Stakeholder engagement** - Familiar boundaries improve result communication and acceptance

**Multi-Iteration Clustering Process**

The clustering methodology supports both single and dual-iteration approaches:

* **First iteration** - Clusters all nodes to desired number of representative nodes
* **Second iteration** (optional) - Further reduces transmission network while preserving renewable resource resolution
* **Resolution constraints** - Transmission network resolution must be larger than or equal to resource resolution

**Multi-Iteration Strategy Rationale**

The two-iteration approach addresses the different spatial scales relevant to renewable resources and transmission infrastructure:

- **Resource-transmission decoupling** - Renewable resources (especially wind and solar) require high spatial resolution to capture local variability, while transmission networks can often be simplified without significant accuracy loss
- **Computational optimization** - Allows users to maintain detailed renewable resource representation while reducing transmission network complexity for faster computation
- **Flexible modeling** - Enables different levels of detail depending on study focus - detailed resources for renewable integration analysis, simplified transmission for capacity planning

**Configuration Guidelines:**
- **High renewable penetration studies** - Use detailed resource resolution with simplified transmission
- **Transmission expansion planning** - Use moderate resource resolution with detailed transmission network
- **Preliminary analysis** - Use simplified resolution for both resources and transmission
- **Detailed operational studies** - Use high resolution for both resources and transmission network

Line Augmentation Techniques
----------------------------

**K-Edge Augmentation Algorithm**

To address connectivity challenges in sparsely connected regional networks, PyPSA-Earth implements advanced line augmentation:

**Connectivity Enhancement**

* **Minimum connectivity guarantee** - Ensures every node has a configurable number of connections
* **Nearest neighbor approach** - Creates new connections using minimum spanning tree algorithms
* **Expandable capacity initialization** - New lines set with minimal capacity (e.g., 1 MW) for optimization
* **Continental interconnection** - Enables exploration of inter-regional transmission opportunities

**Augmentation Strategy Rationale**

The line augmentation approach addresses realistic infrastructure development constraints:

- **Isolated network limitations** - Many regional power systems, particularly in developing regions, lack adequate interconnection, limiting their ability to share resources and improve reliability
- **Investment optimization enablement** - By adding minimal-capacity "placeholder" lines, the optimization can explore transmission expansion options that would otherwise be impossible
- **Realistic infrastructure development** - New connections follow minimum spanning tree logic, reflecting how actual transmission development typically occurs (connecting to nearest feasible points)
- **Scalable connectivity** - The configurable k-edge parameter allows users to adjust network connectivity based on regional characteristics and study objectives

**Configuration Recommendations:**
- **Isolated regional studies** - Use k=2 or k=3 to ensure basic connectivity while maintaining realism
- **Continental interconnection studies** - Use higher k values (k=4-6) to explore extensive regional cooperation scenarios
- **Island nation studies** - Use k=1-2 with careful attention to submarine cable constraints
- **Developed region studies** - Use lower k values since existing networks are typically well-connected

**Network Meshing Benefits**

The augmentation algorithm addresses:

* **Isolated planning limitations** - Overcomes fragmented national grid planning
* **Mini-grid integration** - Connects isolated electrification systems
* **Investment optimization** - Provides transmission expansion options for capacity optimization
* **Reliability improvement** - Enhances network redundancy and resilience

HVAC and HVDC Integration
========================

**Multi-Technology Network Representation**

PyPSA-Earth supports comprehensive modeling of modern transmission systems:

**High Voltage Alternating Current (HVAC)**

* **Voltage level modeling** - Supports multiple voltage levels (110 kV, 220 kV, 380 kV, >380 kV)
* **Circuit representation** - Accounts for single and multiple circuit configurations
* **Transformer integration** - Models voltage level transitions and substation equipment
* **Power flow constraints** - Implements linearized power flow approximations

**High Voltage Direct Current (HVDC)**

* **Long-distance transmission** - Optimized for continental and intercontinental connections
* **Converter modeling** - Represents AC/DC conversion facilities
* **Point-to-point connections** - Supports dedicated HVDC transmission corridors
* **System integration** - Enables hybrid AC/DC network optimization

**Technology Integration Rationale**

The multi-technology approach reflects modern power system realities:

- **Complementary technologies** - HVAC provides regional connectivity and grid stability, while HVDC excels at long-distance, high-capacity transmission with minimal losses
- **Optimal technology selection** - The optimization can choose between HVAC and HVDC based on distance, capacity, and cost considerations, reflecting real-world planning decisions
- **Converter constraints** - Explicit modeling of AC/DC conversion ensures realistic representation of HVDC system limitations and costs
- **System stability** - Maintains AC grid characteristics essential for stability while enabling DC transmission benefits

**Application Scenarios:**
- **Continental interconnection** - HVDC for long-distance connections, HVAC for regional distribution
- **Offshore wind integration** - HVDC for offshore collection and transmission, HVAC for onshore distribution
- **Renewable integration** - Combined AC/DC systems for optimal renewable resource transmission
- **Market coupling** - HVDC links for electricity market integration across large distances

**Cross-Border Interconnections**

The methodology supports:

* **International transmission** - Models cross-border power exchange capabilities
* **Regional integration** - Enables continental-scale power system analysis
* **Market coupling** - Supports electricity market integration studies

Quality Improvement Approaches
==============================

**Data Validation and Cleaning**

Comprehensive quality improvement ensures reliable network representations:

**Coordinate Tolerance Management**

* **GPS accuracy considerations** - Accounts for inherent limitations in OSM coordinate precision
* **Spatial clustering algorithms** - Groups nearby components representing identical infrastructure
* **Geometric consistency** - Ensures realistic spatial relationships between components

**Connectivity Analysis**

* **Network topology validation** - Verifies realistic connectivity patterns
* **Error detection algorithms** - Automated identification of data inconsistencies
* **Correction procedures** - Systematic resolution of detected errors

**Component Integration Quality**

* **Multi-voltage consistency** - Ensures appropriate connections within and between voltage levels
* **Geographic constraint consideration** - Accounts for terrain and infrastructure limitations
* **Redundancy representation** - Maintains multiple transmission paths for reliability analysis

**Validation Framework**

The quality improvement methodology includes:

* **Statistical validation** - Comparison with official transmission system data
* **Topological verification** - Cross-validation with alternative data sources
* **Continuous improvement** - Integration of user feedback and data updates

**Validation Strategy and Limitations**

The validation approach acknowledges inherent challenges in validating crowd-sourced infrastructure data:

- **Reference data limitations** - Official transmission system data is often proprietary or outdated, requiring validation against multiple imperfect sources
- **Regional accuracy variation** - OSM data quality varies significantly by region, with developed countries typically having more complete and accurate infrastructure data
- **Temporal validation challenges** - Infrastructure changes over time, making point-in-time validation difficult for dynamic systems
- **Completeness vs. accuracy trade-off** - Global coverage necessarily involves some accuracy compromises compared to region-specific, professionally curated datasets

**Validation Methodology Applications:**
- **Regional model development** - Intensive validation for specific regions where high-quality reference data is available
- **Global consistency checks** - Statistical validation to identify and correct systematic errors across regions
- **Iterative improvement** - Continuous validation as new reference data becomes available
- **User-contributed validation** - Community-based validation leveraging local knowledge and expertise

**Confidence Assessment:**
- **High confidence regions** - Areas with extensive OSM coverage and available reference data for validation
- **Medium confidence regions** - Areas with good OSM coverage but limited reference data
- **Low confidence regions** - Areas with sparse OSM coverage requiring careful interpretation of results

References
==========

For related information, see:

* :doc:`data_processing` - Data integration workflows
* :doc:`mathematical_framework` - Network constraints in optimization
* :doc:`../data_sources` - Geographic and infrastructure data sources
