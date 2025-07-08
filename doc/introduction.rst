.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _introduction:

##########################################
Introduction
##########################################

What is PyPSA-Earth?
====================

PyPSA-Earth is an open-source energy system optimization model for analyzing and planning energy systems globally. Built on the PyPSA framework, it provides researchers, policymakers, and companies with tools to model energy systems at various scales - from individual countries to entire continents.

**Core Capabilities:**

* **Global Coverage**: Model energy systems for any country or region worldwide
* **Multi-Scale Analysis**: From local city-level studies to continental interconnections
* **High Resolution**: Detailed spatial (substation-level) and temporal (hourly) modeling
* **Sector Integration**: Electricity, heating, transport, industry, and hydrogen systems
* **Open Source**: Transparent methodology with freely available code and data

**Key Features:**

PyPSA-Earth addresses common limitations in energy system modeling by providing:

* **Automated data processing** from open sources like OpenStreetMap and weather databases
* **Network reconstruction** algorithms for building transmission system models
* **Flexible optimization** supporting both operational studies and capacity expansion planning
* **Reproducible workflows** using Snakemake for transparent and collaborative research

**Applications:**

The model has been applied to study energy transitions across Africa, develop net-zero scenarios for various countries, analyze renewable energy integration, and support infrastructure investment decisions. PyPSA-Earth serves as a bridge between academic research and practical energy planning.

Core Features
=============

PyPSA-Earth provides five essential capabilities that make it a versatile tool for energy system analysis:

**1. Flexible Geographic Scope**

Model energy systems at any scale - from individual cities to entire continents. The framework automatically adapts spatial resolution based on study requirements, supporting both local detailed analysis and global interconnection studies.

**2. Automated Data Integration**

Streamlined data processing extracts and integrates information from multiple open sources including OpenStreetMap, weather databases, and energy statistics. This automation eliminates manual data collection and ensures consistent, reproducible model inputs.

**3. High-Resolution Modeling**

Combine detailed spatial resolution (down to substation level) with flexible temporal resolution (hourly to multi-year analysis). Advanced clustering algorithms optimize computational efficiency while preserving essential system characteristics.

**4. Sector Coupling**

Model integrated energy systems covering electricity, heating, transport, industry, and hydrogen sectors. This comprehensive approach captures interactions between sectors essential for analyzing modern energy transitions.

**5. Open Workflow Management**

Transparent, reproducible modeling workflows using Snakemake ensure scientific rigor and enable collaborative development. All code, data sources, and methodologies are openly available for scrutiny and improvement.

For detailed technical information, see :doc:`methodology` and :doc:`data_sources`.

Scenario Analysis and Application Areas
=======================================

PyPSA-Earth supports diverse analytical applications across multiple domains:

**Energy System Analysis**

* **Transition Planning**: Model decarbonization pathways, renewable integration, and technology transitions
* **Operational Studies**: Optimize system operation, assess grid constraints, and evaluate security of supply
* **Expansion Planning**: Determine optimal infrastructure investments and technology deployment strategies

**Policy and Investment Support**

* **Policy Analysis**: Evaluate climate policies, market designs, and regulatory impacts on energy systems
* **Investment Planning**: Support both public infrastructure planning and private sector investment decisions
* **Technology Assessment**: Compare energy technologies, storage systems, and sector coupling options

**Research Applications**

* **Scenario Analysis**: Explore multiple futures using advanced uncertainty quantification methods
* **System Integration**: Study interactions between electricity, heating, transport, and industrial sectors
* **Regional Studies**: Analyze energy systems from local to continental scales with consistent methodology

PyPSA-Earth has been successfully applied to validate models across Africa, develop net-zero scenarios for various countries, analyze renewable energy integration challenges, and support infrastructure investment decisions worldwide.

For detailed application examples and methodologies, see :doc:`capabilities`.

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
  url = {https://www.sciencedirect.com/science/article/pii/S0306261923004609},
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
