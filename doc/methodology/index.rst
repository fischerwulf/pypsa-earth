.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _methodology:

##########################################
Methodology
##########################################

Overview
========

PyPSA-Earth employs a comprehensive methodology for global energy system modeling that combines automated data processing, sophisticated mathematical optimization, and rigorous validation frameworks. This methodology section provides detailed technical documentation of the approaches, algorithms, and workflows that enable PyPSA-Earth to model energy systems at any scale with high spatial and temporal resolution.

The methodology is organized into five key components:

**Data Processing**
    Comprehensive workflows for integrating weather data, renewable energy resources, and demand patterns.

**Data Sources and Integration**
    Comprehensive data infrastructure with systematic quality assurance, uncertainty quantification, and integration frameworks.

**Network Modeling**
    Automated approaches for constructing realistic power system networks from open-source geospatial data.

**Mathematical Framework**
    The core optimization formulations, objective functions, and constraints that define the energy system modeling problem.

**Workflow Management**
    Reproducible and transparent processing pipelines using Snakemake for automated model building.

**Validation Framework**
    Quality assurance procedures and performance validation methods to ensure model accuracy.

These methodological components work together to create a robust, transparent, and globally applicable energy system modeling framework that supports both research and practical applications.

Methodological Components
=========================

.. toctree::
   :maxdepth: 2

   data_processing
   data_sources
   network_modeling
   mathematical_framework
   workflow_management
   validation_framework

Integration with PyPSA-Earth Workflow
=====================================

The methodology described in this section is implemented through PyPSA-Earth's automated workflow system. For practical application guidance, see:

* :doc:`../introduction` - Overview of capabilities and applications
* :doc:`../tutorial_electricity` - Step-by-step modeling tutorials
* :doc:`../tutorial_sector` - Sector-coupled modeling examples

For the complete technical foundation, we recommend following the methodology sections in order, as each builds upon concepts from previous sections.
