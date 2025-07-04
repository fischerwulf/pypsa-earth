.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _introduction:

##########################################
Introduction
##########################################

What is PyPSA-Earth?
====================

PyPSA-Earth is a powerful open-source energy system optimization model that enables researchers, policymakers, and companies to analyze and plan energy systems anywhere in the world. Unlike traditional "black-box" models that are expensive and lack transparency, PyPSA-Earth provides a completely open platform for energy system modeling with unprecedented flexibility and global coverage.

**Key Capabilities:**

* **Global Scope with Local Detail**: Model the entire world's energy system or zoom in to study specific countries, regions, or even individual cities
* **High Resolution**: Analyze energy systems with detailed spatial resolution (down to individual substations) and temporal resolution (hourly or sub-hourly data)
* **Comprehensive Analysis**: Perform various types of studies including energy transition scenarios, technology evaluations, policy assessments, and investment planning
* **Transparent and Reproducible**: All code, data sources, and methods are openly available, ensuring scientific rigor and enabling collaboration

**Why PyPSA-Earth Matters:**

The global energy transition requires sophisticated planning tools that can handle the complexity of modern energy systems. PyPSA-Earth addresses critical gaps in existing models:

* **Transparency**: Unlike proprietary models, every assumption and calculation is open for scrutiny and improvement
* **Global Coverage**: Most energy models focus on specific regions; PyPSA-Earth can model any part of the world with consistent methodology
* **Collaboration**: The open-source nature enables researchers worldwide to contribute improvements that benefit everyone
* **Accessibility**: Free to use, removing financial barriers that prevent many organizations from accessing advanced energy modeling tools

**What Makes PyPSA-Earth Unique:**

PyPSA-Earth combines cutting-edge data processing with proven optimization techniques:

* **Automated Data Processing**: Automatically extracts and processes energy system data from open sources like OpenStreetMap
* **Advanced Network Modeling**: Reconstructs electrical transmission networks using novel algorithms designed for global coverage
* **Flexible Optimization**: Supports both operational studies (how to run existing systems) and expansion planning (what new infrastructure to build)
* **Sector Coupling**: Can model not just electricity, but also heating, transport, and hydrogen systems

**Real-World Applications:**

PyPSA-Earth has been successfully applied to:

* Validate energy system models across the entire African continent
* Develop net-zero emission scenarios for countries like Nigeria
* Analyze renewable energy potentials and grid integration challenges
* Support policy decisions for energy infrastructure investments

The model serves as a bridge between academic research and practical energy planning, providing the analytical foundation needed to accelerate the global energy transition.

Core Features
=============

PyPSA-Earth offers a comprehensive suite of features designed to meet the diverse needs of energy system modeling. Below are the key capabilities that make PyPSA-Earth a powerful tool for energy analysis.

Flexible Modeling Scope
------------------------

**From Global to Local Analysis**

PyPSA-Earth's most distinctive feature is its ability to seamlessly scale from global analysis down to local detail:

* **Global Modeling**: Analyze worldwide energy systems, continental interconnections, and international energy trade
* **Regional Focus**: Study multi-country regions like Africa, Europe, or Southeast Asia with detailed cross-border interactions
* **National Planning**: Model individual countries with high spatial resolution for national energy policy development
* **Subnational Analysis**: Examine states, provinces, or metropolitan areas for targeted regional planning
* **Local Studies**: Focus on specific cities, industrial clusters, or rural electrification projects

**Adaptive Resolution**: The model automatically adjusts its complexity based on your study area. A global study might use country-level aggregation, while a national study can resolve individual substations and transmission lines.

**Seamless Integration**: Results from global studies can inform regional models, and local insights can be scaled up to inform larger policy decisions.

Automated Data Processing
--------------------------

**Intelligent Data Extraction**

PyPSA-Earth revolutionizes energy modeling through its automated data processing pipeline:

* **OpenStreetMap Integration**: Automatically extracts electrical transmission networks, substations, and power plant locations from the world's most comprehensive open geographic database
* **Multi-Source Data Fusion**: Combines data from satellite imagery, weather databases, economic statistics, and energy databases to create comprehensive energy system representations
* **Real-Time Updates**: Leverages daily-updated OpenStreetMap data to ensure models reflect the latest infrastructure developments
* **Quality Assurance**: Automated data cleaning and validation processes ensure high-quality inputs for reliable modeling results

**Supported Data Sources**:

* **Weather Data**: ERA5 reanalysis data for wind and solar resource assessment
* **Demand Projections**: Socioeconomic pathway scenarios for future energy demand
* **Infrastructure Data**: Power plant databases, transmission line information, and renewable energy installations
* **Economic Data**: Technology costs, fuel prices, and policy parameters

**User-Friendly Configuration**: Simply specify your region of interest and study parameters – PyPSA-Earth handles the complex data processing automatically.

High Spatial and Temporal Resolution
------------------------------------

**Detailed Spatial Modeling**

PyPSA-Earth provides unprecedented spatial detail in energy system modeling:

* **Substation-Level Detail**: Model individual electrical substations and their interconnections
* **Administrative Boundaries**: Align models with political boundaries for policy-relevant analysis
* **Voronoi Tessellation**: Create optimal spatial partitions based on electrical network topology
* **Flexible Aggregation**: Dynamically adjust spatial resolution based on computational resources and study requirements

**Temporal Precision**

The model supports various temporal resolutions to match your analytical needs:

* **Hourly Resolution**: Standard for most energy system analyses, capturing daily demand patterns and renewable variability
* **Sub-Hourly Analysis**: Model fast-response systems like battery storage and grid frequency regulation
* **Multi-Year Planning**: Analyze long-term capacity expansion and technology transition pathways
* **Representative Periods**: Efficiently handle long-term studies using carefully selected time periods

**Clustering Strategies**: Advanced algorithms reduce computational complexity while preserving essential system characteristics.

Scenario Analysis and Application Areas
=======================================

**Comprehensive Analysis Framework**

PyPSA-Earth enables sophisticated scenario analysis across multiple application domains, providing decision-makers with the tools needed to plan the energy transition effectively.

Energy System Studies
---------------------

**Energy Transition Analysis**

*Decarbonization Pathways*:
* Model pathways to achieve net-zero emissions targets with intermediate milestones
* Analyze renewable integration and variable energy source impacts on system stability
* Study technology transition from fossil fuels to clean energy alternatives
* Evaluate system flexibility needs including storage, demand response, and sector coupling

*Operational Studies*:
* Optimize daily and seasonal operation of existing energy infrastructure
* Assess transmission constraints and power flow limitations under different conditions
* Evaluate system adequacy and security of supply scenarios
* Model electricity market operations and price formation mechanisms

*Expansion Planning*:
* Determine optimal locations and timing for new generation and transmission capacity
* Identify critical transmission bottlenecks and design grid reinforcement strategies
* Optimize future technology portfolios considering cost, reliability, and environmental objectives
* Evaluate optimal deployment of different storage technologies across the system

Technology Evaluation
----------------------

**Comprehensive Technology Assessment**

*Energy Storage Technologies*:
* Battery storage: lithium-ion, flow batteries, and other electrochemical systems
* Pumped hydro storage potential in different geographical contexts
* Hydrogen production, storage, and utilization for long-term energy storage
* Thermal storage for heating and cooling applications

*Renewable Energy Technologies*:
* Solar PV: utility-scale and distributed photovoltaic deployments
* Wind power: onshore and offshore potential and integration challenges
* Hydroelectric: existing and potential resources including run-of-river and reservoir systems
* Emerging technologies: concentrated solar power, geothermal, and other renewables

*Sector Coupling Technologies*:
* Heat pump deployment for heating electrification
* Electric vehicle charging infrastructure integration
* Hydrogen economy: production, transport, and utilization pathways
* Synthetic fuels production for aviation, shipping, and industrial applications

*Technology Phase-Out Planning*:
* Coal plant retirement: optimal timing and replacement strategies
* Nuclear decommissioning implications on system reliability and costs
* Natural gas infrastructure transition to hydrogen or other clean alternatives

Policy Analysis
---------------

**Evidence-Based Policy Support**

*Climate Policy*:
* Carbon pricing: taxes, cap-and-trade systems, and border carbon adjustments
* Emissions trading scheme effects on technology deployment and costs
* Climate target feasibility and cost assessment
* Just transition: social and economic implications of energy transition policies

*Energy Security*:
* Supply diversification strategies to reduce import dependence
* Strategic reserves and emergency measures modeling
* Critical infrastructure vulnerability to disruptions and climate risks
* Energy independence pathway analysis

*Market Design*:
* Electricity market structure impacts on investment incentives and system efficiency
* Renewable support mechanisms: feed-in tariffs, portfolio standards, and other policies
* Technical regulation impacts on renewable energy integration
* Capacity market mechanisms and their effect on system adequacy

*Regulatory Impact Assessment*:
* Environmental regulation impacts on the energy sector
* Energy efficiency standards effects on electricity demand
* Electric vehicle mandates and transport electrification policy impacts

Investment Planning
--------------------

**Strategic Investment Analysis**

*Public Sector Investment*:
* Infrastructure planning: transmission and distribution priority investments
* Public utility investment strategy optimization
* Development bank and agency energy sector investment prioritization
* Rural electrification and energy access program planning

*Private Sector Investment*:
* Generation investment opportunities in renewable and conventional energy
* Grid investment: transmission and distribution opportunities
* Technology investment: venture capital and private equity in energy technologies
* Investment risk quantification: regulatory, market, and technology risks

*Financial Analysis*:
* Economic viability evaluation of energy projects and policies
* Financing mechanism modeling: public-private partnerships and other structures
* Revenue forecasting: electricity prices and technology revenue streams
* Investment sensitivity to key parameters: fuel costs and carbon prices

*Portfolio Optimization*:
* Energy asset portfolio optimization considering risk-return profiles
* Geographic and technology diversification strategies
* Investment timing optimization based on market conditions and policy changes
* Asset retirement and replacement decision modeling

*Regional Development*:
* Regional energy hub opportunities for trading and cooperation
* Industrial cluster energy infrastructure planning
* Urban energy infrastructure integration with development planning
* Rural distributed energy solutions for economic development

Uncertainty Analysis
---------------------

**Risk Assessment Methods**

*Advanced Analysis Techniques*:
* Monte Carlo simulations to quantify uncertainty in model outputs
* Sensitivity analysis to identify key parameters driving results
* Robust optimization to find solutions performing well across multiple scenarios
* Scenario planning with coherent storylines combining multiple uncertainties

*Economic Scenario Analysis*:
* Cost trajectory modeling: declining renewable costs and changing fuel prices
* Investment pattern analysis: public vs. private infrastructure investment
* Market design assessment: different electricity market structures and pricing mechanisms

Data Sources and Methodology
=============================

**Advanced Data Processing and Integration**

PyPSA-Earth's strength lies in its sophisticated data processing capabilities that automatically integrate multiple open data sources to create comprehensive energy system models.

Network Topology and Infrastructure
------------------------------------

**OpenStreetMap-Based Network Reconstruction**

PyPSA-Earth employs a novel approach to reconstruct electrical transmission networks using OpenStreetMap (OSM) data:

*Three-Step Network Creation Process*:
* **Data Download**: Fast retrieval of OSM data through multi-threaded processing using the esy-osm tool
* **Filtering and Cleaning**: Automated cleaning of geospatial descriptions and alignment with PyPSA framework requirements
* **Network Building**: Construction of meshed network datasets with transformers, substations, converters, and high voltage AC/DC components

*Network Components*:
* Substations and transformers from OSM feature extraction
* High voltage alternating current (HVAC) transmission lines
* High voltage direct current (HVDC) transmission systems
* Power line geospatial descriptions with coordinate tolerance improvements

**Fundamental Spatial Shapes**

The model creates spatial regions for data aggregation through two complementary approaches:

*Onshore Regions*:
* **Global Administrative Areas (GADM)**: Administrative zones at various levels (national, regional, provincial, municipal)
* **Voronoi Partitioning**: Areas created from substation GIS locations with boundaries equidistant to nearest sites

*Offshore Regions*:
* **Maritime Boundaries**: Voronoi areas built from high voltage onshore nodes
* **Exclusive Economic Zones (EEZ)**: Offshore extent limitations based on country-specific maritime data

Renewable Energy Resource Assessment
-------------------------------------

**Atlite Integration for Weather-Dependent Resources**

PyPSA-Earth leverages the Atlite package for comprehensive renewable energy modeling:

*Data Processing Workflow*:
* **Cutout Creation**: Define spatio-temporal boundaries for analysis regions
* **Data Preparation**: Integration of environmental and weather data from multiple sources
* **Technology Conversion**: Application of technology-specific models to generate time series and potentials

*Supported Data Sources*:
* **ERA5 Reanalysis Data**: High-quality weather data for wind and solar resource assessment
* **SARAH-2 Satellite Data**: Solar radiation data for photovoltaic modeling
* **GEBCO Bathymetry**: Offshore depth data for wind farm siting

*Technology Coverage*:
* Solar photovoltaic systems (utility-scale and distributed)
* Onshore and offshore wind turbines
* Hydroelectric resources (run-of-river, reservoir, and dam systems)
* Future expansion capabilities for concentrated solar power and thermal collectors

**Power Density and Land Use Constraints**

The model employs conservative socio-technical power density assumptions:

*Solar PV*: 4.6 MW/km² (10% of average power plant density of 46.4 MW/km²)
*Onshore Wind*: 3 MW/km² (reduced from technical density of 6.2 MW/km²)
*Offshore Wind*: 2 MW/km² (reduced from technical density of 4 MW/km²)

*Land Use Exclusions*:
* Protected and reserved areas from protectedplanet.net
* Specific land-cover types from Copernicus Global Land Service
* Technology-dependent eligibility criteria

Electricity Demand Modeling
----------------------------

**Global Demand Predictions**

PyPSA-Earth provides comprehensive electricity demand forecasting capabilities:

*Temporal Coverage*:
* Hourly demand predictions for future scenarios
* Multiple weather years (2011, 2013, 2018) for climate variability
* Long-term projections for 2030, 2040, 2050, and 2100

*Methodology*:
* **GEGIS Integration**: Global Energy GIS package for demand time series creation
* **Machine Learning Approach**: Predictors include temperature, population, GDP, industrial structure, and technology adoption
* **Socioeconomic Pathways**: Shared Socioeconomic Pathways (SSP) scenarios for future projections

*Validation and Accuracy*:
* 8% absolute error across 44 countries in validation tests
* Regional scaling for countries with limited data availability
* Population and GDP proportional scaling methods

Power Plant Database Enhancement
--------------------------------

**Extended Powerplantmatching Tool**

PyPSA-Earth enhances the existing powerplantmatching tool with additional data sources:

*Data Integration Process*:
* **Multi-Source Compilation**: Integration of various open data sources including ENTSO-E, GEO, and IRENA statistics
* **Duplicate Detection**: Pairwise comparison algorithms to identify and remove duplicated entries
* **OpenStreetMap Enhancement**: Novel inclusion of OSM data for improved African power plant coverage

*Quality Assurance*:
* 90% accuracy validation against commercial databases in Europe
* Enhanced coverage for regions with limited data availability
* Continuous data quality improvement through open-source collaboration

Advanced Preprocessing Techniques
----------------------------------

**Spatial Clustering Strategies**

PyPSA-Earth offers multiple clustering methods to balance model accuracy with computational efficiency:

*Clustering Approaches*:
* **Renewable Potential Focused**: Hierarchical clustering based on capacity factors and load patterns
* **Transmission Grid Focused**: Density-based clustering using line impedance metrics
* **Geographic Clustering**: Weighted k-means algorithm on network node locations
* **Administrative Clustering**: Aggregation based on GADM administrative boundaries

*Two-Iteration Framework*:
* **First Iteration**: Aggregation of all network components to desired resolution
* **Second Iteration**: Optional further network reduction while preserving renewable resource resolution

**Network Augmentation**

To address connectivity limitations in developing regions:

*K-Edge Augmentation Algorithm*:
* Ensures minimum connectivity requirements for all network nodes
* Creates new transmission options through minimum spanning tree approach
* Enables exploration of interconnected continental scenarios
* Supports investment optimization in transmission expansion

Workflow Management and Reproducibility
----------------------------------------

**Snakemake Integration**

PyPSA-Earth employs sophisticated workflow management for reproducible research:

*Workflow Features*:
* **Modular Design**: Decomposition of complex processes into manageable subtasks
* **Dependency Tracking**: Automatic execution order based on input/output relationships
* **Incremental Updates**: Selective regeneration when data or scripts are modified
* **Single Command Execution**: Complete workflow execution with simple commands

*Benefits*:
* Enhanced user and developer experience
* Improved maintainability and transparency
* Facilitated collaborative development
* Ensured reproducible scientific results

Mathematical Modeling Framework
================================

**Optimization Problem Formulation**

PyPSA-Earth formulates energy system planning as a linear optimization problem that minimizes total system costs while satisfying physical and operational constraints.

**Objective Function**

The model minimizes the total Annualized Costs (AC) of the energy system:

.. math::

   \min AC = \sum_{i,r} (c_{i,r} \cdot G_{i,r}) + \sum_l (c_l \cdot F_l) + \sum_{i,s} (c_{i,s}^{store} \cdot H_{i,s}^{store} + c_{i,s}^- \cdot H_{i,s}^- + c_{i,s}^+ \cdot H_{i,s}^+) + \sum_{i,r,t} (o_{i,r} \cdot g_{i,r,t} \cdot w_t) + \sum_{i,s,t} ((o_{i,s}^+ \cdot h_{i,s,t}^+ + o_{i,s}^- \cdot h_{i,s,t}^-) \cdot w_t) + \sum_{i,s,t} (o_{i,s}^{store} \cdot e_{i,s,t} \cdot w_t)

**Cost Components**

*Capital Expenditures (CAPEX)*:
* Generation capacity investments: Installing new power plants and renewable generators
* Storage system investments: Energy capacity, charging, and discharging equipment
* Transmission infrastructure: New power lines and grid reinforcements

*Operational Expenditures (OPEX)*:
* Variable generation costs: Fuel costs, operation and maintenance
* Storage operation costs: Charging, discharging, and energy level maintenance
* Time-weighted costs: Accounting for different operational periods throughout the year

**Physical and Operational Constraints**

The optimization is subject to multiple constraint categories that ensure realistic system operation:

**Energy Balance Constraints**

*Kirchhoff's Current Law* - ensures energy balance at every network node:

.. math::

   \sum_r g_{i,r,t} - \sum_s h_{i,s,t}^+ + \sum_s h_{i,s,t}^- + \sum_l K_{i,l} \cdot f_{l,t} = d_{i,t}

where generation, storage charging/discharging, and power flows must exactly meet demand at each location and time.

*Kirchhoff's Voltage Law* - maintains voltage angle consistency in AC networks:

.. math::

   \sum_l C_{l,c} \cdot x_l \cdot f_{l,t} = 0

This constraint ensures that voltage angle differences around closed network cycles sum to zero, representing the physics of power flow.

**Capacity Constraints**

*Installation Limits*:
* Generator capacity bounds: :math:`\underline{G}_{i,r} \leq G_{i,r} \leq \overline{G}_{i,r}`
* Storage capacity bounds: :math:`\underline{H}_{i,s} \leq H_{i,s} \leq \overline{H}_{i,s}`
* Transmission capacity bounds: :math:`\underline{F}_l \leq F_l \leq \overline{F}_l`

*Operational Limits*:
* Renewable generation availability: :math:`0 \leq g_{i,r,t} \leq \overline{g}_{i,r,t} \cdot G_{i,r}`
* Storage charging/discharging rates: :math:`0 \leq h_{i,s,t}^{\pm} \leq H_{i,s}^{\pm}`
* Power flow limits: :math:`0 \leq f_{l,t} \leq \overline{f}_{l,t} \cdot F_l`

**Storage Modeling**

*Energy Balance*:

.. math::

   e_{i,s,t} = \eta_{i,s}^{store} \cdot e_{i,s,t-1} + \eta_{i,s}^+ \cdot w_t \cdot h_{i,s,t}^+ - \eta_{i,s}^{-1} \cdot w_t \cdot h_{i,s,t}^- + w_t \cdot h_{i,s,t}^{inflow} - w_t \cdot h_{i,s,t}^{spillage}

*Storage Constraints*:
* Energy capacity limits: :math:`0 \leq e_{i,s,t} \leq H_{i,s}^{store}`
* Cyclic operation: :math:`e_{i,s,0} = e_{i,s,T}` (storage levels must return to initial state)
* Technology-specific energy-to-power ratios: :math:`0 \leq e_{i,s,t} \leq T^s \cdot H_{i,s}^-`

**Environmental Constraints**

*Emissions Limits*:

.. math::

   \sum_{i,r,t} g_{i,r,t} \cdot \gamma_r \leq GHG

where :math:`\gamma_r` represents the emission intensity of technology :math:`r` and :math:`GHG` is the total allowable emissions.

**Solution Properties**

*Linear Programming Advantages*:
* Convex optimization problem ensures global optimality
* Efficient solution algorithms can handle large-scale problems
* Unique objective value with potentially multiple operational solutions
* Computational tractability for multi-year, high-resolution studies

*High-Resolution Modeling*:
* Temporal resolution: Hourly optimization over full years (8,760 hours)
* Spatial resolution: Node-level detail based on transmission network topology
* Technology detail: Explicit representation of individual generation and storage technologies

Video and Milestone Paper
========

A short video explaining the logic of PyPSA-Eur which is similar to PyPSA-Earth:

.. raw:: html

    <iframe width="832" height="468" src="https://www.youtube.com/embed/ty47YU1_eeQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For more details on PyPSA-Earth read the below milestone paper.
For citations, please use the following BibTeX: ::

  @misc{PyPSAEarth,
  author = {Parzen, Maximilian and Abdel-Khalek, Hazem and Fedorova, Ekaterina and Mahmood, Matin and Frysztacki, Martha Maria and Hampp, Johannes and Franken, Lukas and Schumm, Leon and Neumann, Fabian and Poli, Davide and Kiprakis, Aristides and Fioriti, Davide},
  title = {PyPSA-Earth. A new global open energy system optimization model demonstrated in Africa},
  publisher = {Applied Energy},
  year = {2023},
  url = {https://www.sciencedirect.com/science/article/pii/S030626192300460},
  doi = {https://doi.org/10.1016/j.apenergy.2023.121096},
  }


Workflow
========

The generation of the model is controlled by the workflow management system `Snakemake <https://snakemake.bitbucket.io/>`_. In a nutshell,
the ``Snakefile`` declares for each python script in the ``scripts`` directory a rule which describes which files the scripts consume and
produce (their corresponding input and output files). The ``snakemake`` tool then runs the scripts in the correct order according to the
rules' input/output dependencies. Moreover, it is able to track, what parts of the workflow have to be regenerated, when a data file or a
script is modified/updated. For example, by executing the following snakemake routine

.. code:: bash

    .../pypsa-earth % snakemake -j 1 networks/elec_s_128.nc

the following workflow is automatically executed.

.. image:: img/workflow_introduction.png
    :align: center

The **blocks** represent the individual rules which are required to create the file ``networks/elec_s_128.nc``.
Each rule requires scripts (e.g. Python) to convert inputs to outputs.
The **arrows** indicate the outputs from preceding rules which a particular rule takes as input data.

.. note::
    For reproducibility purposes, the image can be obtained through
    ``snakemake --dag networks/elec_s_128.nc | dot -Tpng -o workflow.png``
    using `Graphviz <https://graphviz.org/>`_


Folder structure
================

The content in this package is organized in folders as described below; for more details, please see the documentation.

- ``data``: Includes input data that is not produced by any ``snakemake`` rule.
- ``scripts``: Includes all the Python scripts executed by the ``snakemake`` rules.
- ``resources``: Stores intermediate results of the workflow which can be picked up again by subsequent rules.
- ``networks``: Stores intermediate, unsolved stages of the PyPSA network that describes the energy system model.
- ``results``: Stores the solved PyPSA network data, summary files and plots.
- ``benchmarks``: Stores ``snakemake`` benchmarks.
- ``logs``: Stores log files about solving, including the solver output, console output and the output of a memory logger.
- ``envs``: Stores the conda environment files to successfully run the workflow.


License
=======

PyPSA-Earth work is released under multiple licenses:

* All original source code is licensed as free software under `AGPL-3.0 License <https://github.com/pypsa-meets-earth/pypsa-earth/blob/main/LICENSES>`_.
* The documentation is licensed under `CC-BY-4.0 <https://creativecommons.org/licenses/by/4.0/>`_.
* Configuration files are mostly licensed under `CC0-1.0 <https://creativecommons.org/publicdomain/zero/1.0/>`_.
* Data files are licensed under different licenses as noted below.

Individual files contain license information in the header or in the `dep5 <.reuse/dep5>`_.
Additional licenses and urls of the data used in PyPSA-Earth:

.. csv-table::
   :header-rows: 1
   :file: configtables/licenses.csv


* *BY: Attribute Source*
* *NC: Non-Commercial Use Only*
* *SA: Share Alike*
