.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _installation:

##########################################
Installation
##########################################

This guide provides comprehensive instructions for installing PyPSA-Earth on your system. Choose the installation method that best suits your needs:

* **Standard Installation** (recommended): Using Conda/Mamba
* **Alternative Installation**: Using Docker containers

Before starting, ensure your system meets the hardware and software requirements outlined below.

Hardware Requirements
=====================
Ensure that your system meets the minimum hardware specifications to run PyPSA-Earth effectively:

**Minimum Requirements:**
* **RAM**: 8-16 GB
* **CPU**: At least 2 cores
* **Storage**: Depends on the region of interest:
  
  - **Africa model**: 40 GB
  - **World model**: 250 GB
  - **Single country**: 1-10 GB
  - **Tutorial**: 2 GB
  
  **We recommend at least 40 GB of free storage space** to account for software tools and temporary files.


Software Prerequisites
======================
Before installing PyPSA-Earth, ensure the following software tools are installed on your system:

**Required:**
* `Miniconda <https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html>`_ or `Anaconda <https://www.anaconda.com/download>`_
* `Git <https://git-scm.com/downloads>`_
* `Java <https://www.oracle.com/java/technologies/downloads/>`_ (JDK 17 or JDK 21)

**Optional but Recommended:**
* `VSCode <https://code.visualstudio.com/>`_ or another IDE of your choice

Miniconda
---------
To use packages in Python, it is highly recommended to use a ``conda`` package manager, such as `miniconda <https://docs.conda.io/projects/miniconda/en/latest/>`__. You can check if ``conda`` is already installed on your system with:

.. code:: bash

    $ conda --version

If ``conda`` is not installed, follow the `miniconda installation guide <https://docs.conda.io/projects/conda/en/latest/user-guide/install/>`_.
For more information on how to install conda and work with it, you can look into :ref:`software_hints`.

Git
---
`Git <https://git-scm.com/>`__ is a free open-source tool that facilitates tracking changes in code development and enables coordination of parallel software development between multiple developers.
Download and install ``git`` on your system using the following `link <https://git-scm.com/downloads>`__.
It is highly recommended to `learn the git basics <https://git-scm.com/doc>`__.

VSCode
------
To write and debug Python code, you need an Integrated Development Environment (IDE), which is software used to write code. We recommend `Visual Studio Code <https://code.visualstudio.com/>`_, which is freely available and provides an easy-to-use interface with Git integration. Alternatives like `PyCharm <https://www.jetbrains.com/pycharm/>`_ or `Sublime Text <https://www.sublimetext.com/>`_ will work as well.

Java
----
PyPSA-Earth requires Java to work properly. **Java 17 or Java 21 is recommended** for best compatibility.

**Check if Java is installed:**

.. code:: bash

    $ java --version

**Expected output:**

.. code:: bash

    java version "1.8.0_341"
    Java(TM) SE Runtime Environment (build 1.8.0_341-b10)
    Java HotSpot(TM) 64-Bit Server VM (build 25.341-b10, mixed mode)

**Installation:**

If Java is not installed, download and install it from:
- `Oracle JDK <https://www.oracle.com/java/technologies/downloads/>`_ (commercial)
- `OpenJDK <https://adoptium.net/>`_ (free)

Choose **JDK 17** or **JDK 21** based on your system requirements.

=================
Quick Start Guide
=================

For experienced users who want to get started quickly:

.. code:: bash

    # Clone the repository
    git clone https://github.com/pypsa-meets-earth/pypsa-earth.git
    cd pypsa-earth

    # Install mamba (if not already installed)
    conda install -c conda-forge mamba

    # Create environment (choose appropriate lock file for your platform)
    mamba env create -f envs/linux-64.lock.yaml  # Linux
    # mamba env create -f envs/osx-64.lock.yaml    # macOS Intel
    # mamba env create -f envs/osx-arm64.lock.yaml # macOS Apple Silicon
    # mamba env create -f envs/win-64.lock.yaml    # Windows

    # Activate environment
    conda activate pypsa-earth

    # Verify installation
    snakemake --version

For detailed instructions and troubleshooting, continue reading the sections below.


Installation with Conda/Mamba
===============================

Clone the Repository
--------------------
.. note::

  In order to work with the provided Jupyter notebooks in the `documentation repository <https://github.com/pypsa-meets-earth/documentation>`__, it is recommended to follow the folder structure suggested in :ref:`notebooks`.

First, clone the `PyPSA-Earth repository <https://github.com/pypsa-meets-earth/pypsa-earth/>`__ using the version control system ``git``.

.. important::
   The path to the directory where the ``git repository`` is cloned must **not** contain any spaces.

The following commands can be executed in the command prompt of ``miniconda``, terminal of ``VSCode``, or in ``Git Bash``:

.. code:: bash

    $ git clone https://github.com/pypsa-meets-earth/pypsa-earth.git
    $ cd pypsa-earth

.. note::

    Make sure you are in the ``pypsa-earth`` root directory. You can check this with the ``pwd`` command on Linux/macOS or the ``cd`` command on Windows.
    If you are in the wrong directory, navigate to the ``pypsa-earth`` root directory with ``cd path/to/pypsa-earth``.


Install Dependencies
--------------------
PyPSA-Earth relies on a set of Python packages to function properly.

The Python package requirements are located in the `envs/environment.yaml <https://github.com/pypsa-meets-earth/pypsa-earth/blob/main/envs/environment.yaml>`_ file. We install only `mamba` in the conda base environment to accelerate the installation.

.. important::
   **Please keep the base environment clean by not installing anything else there!** This ensures compatibility of all packages needed to work with the PyPSA-Earth model.

There are also regularly updated locked environment files for
each platform generated with conda-lock to ensure reproducibility. Choose the correct file for your platform:

.. list-table::
   :header-rows: 1
   :widths: 20 40 40

   * - Platform
     - Architecture
     - Lock File
   * - Linux
     - Intel/AMD (x86_64)
     - ``envs/linux-64.lock.yaml``
   * - macOS
     - Intel (x86_64)
     - ``envs/osx-64.lock.yaml``
   * - macOS
     - Apple Silicon (ARM64)
     - ``envs/osx-arm64.lock.yaml``
   * - Windows
     - Intel/AMD (x86_64)
     - ``envs/win-64.lock.yaml``
   * - Other
     - Any
     - ``envs/environment.yaml`` (not locked)

We recommend using the locked files for stability and reproducibility.

**Installation Steps:**

1. **Install Mamba** (faster than conda):

   .. code:: bash

       $ conda install -c conda-forge mamba

2. **Create Environment** (replace with your platform's lock file):

   .. code:: bash

       $ mamba env create -f envs/linux-64.lock.yaml  # Example for Linux

3. **Activate Environment**:

   .. code:: bash

       $ conda activate pypsa-earth

4. **Verify Installation**:

   .. code:: bash

       $ snakemake --version

Environment installation with mamba usually takes about 10-20 minutes. 

.. note::
   Activation is local to the currently open shell. Every time you open a new terminal window, the `pypsa-earth` environment should be activated again to supply the workflow with all the dependencies it needs.

*Alternative Installation Methods:**

If the standard installation doesn't work:

1. **Using Conda instead of Mamba**:

   .. code:: bash

       $ conda env create -f envs/linux-64.lock.yaml
       $ conda activate pypsa-earth

2. **Using Generic Environment File** (if lock file unavailable):

   .. code:: bash

       $ conda install -c conda-forge mamba
       $ mamba env create -f envs/environment.yaml
       $ conda activate pypsa-earth

.. warning::
   The generic environment file may lead to compatibility issues.


Generating the Lock Files (Advanced Users)
---------------------------

If you wish to generate lock-files for your platform, you can use the following commands:

1. Ensure ``conda-lock`` is installed:

   .. code-block:: bash

      $ conda install conda-lock -c conda-forge

2. Generate lock files for target platforms:

   .. code-block:: bash

      $ conda-lock lock -p <your-platform> -k env -f envs/environment.yaml

For platform codes, refer to the `conda-lock documentation <https://conda.github.io/conda-lock/>`_ or use ``conda info`` to determine your platform.

.. seealso::

    For more information on how to install conda and work with it, you can look into :ref:`software_hints`.

To confirm the installation, run the following command in the activated environment:

.. code:: bash

    $ snakemake --version


Solver Installation
-------------------
An optimization solver is needed to solve the mathematical problems that are built with the automated workflow of PyPSA-Earth.
With the goal of supporting a completely open-source initiative, we focus on relying on open-source solvers, such as:

* `CBC <https://projects.coin-or.org/Cbc>`_
* `GLPK <https://www.gnu.org/software/glpk/>`_ and `WinGLPK <http://winglpk.sourceforge.net/>`_ (included in the pypsa-earth environment and installed automatically during environment creation)
* `HiGHS <https://github.com/ERGO-Code/HiGHS>`_ (installed automatically as a dependency for PyPSA)

To further improve performance, commercial solvers like:

* `Gurobi <http://www.gurobi.com/>`_ (the Gurobi package is pre-installed in the environment, but you must obtain and activate your own license; see the `Gurobi documentation <https://www.gurobi.com/documentation/>`_ for details)
* `CPLEX <https://www.ibm.com/analytics/cplex-optimizer>`_

(both commercial licenses with free academic options) can also be used.

.. note::

    ``glpk``, ``gurobi``, and ``highs`` are installed automatically with the environment.
    However, solving capabilities of ``glpk`` are limited.
    To run the model with high temporal and spatial resolution, it is recommended to use ``cplex``, ``gurobi``, or ``highs``.

**Important Notes:**

.. note::
   - Environment installation typically takes 10-20 minutes
   - You can check your platform with ``conda info``
   - The environment must be activated in each new terminal session
   - Keep your conda base environment clean for compatibility

.. tip::
   **Environment Activation Reminder**: Every time you open a new terminal, run:
   
   .. code:: bash
   
       $ conda activate pypsa-earth


Install Jupyter Lab
===================

We use Jupyter notebooks to share examples on how to use the model and analyze the results. ``VSCode`` supports working with Jupyter Notebooks natively. If you are using a different IDE and don't have Jupyter notebooks pre-installed, you can install Jupyter Lab with the `ipython kernel installation <http://echrislynch.com/2019/02/01/adding-an-environment-to-jupyter-notebooks/>`_ and test if Jupyter Lab works:

.. code:: bash

    $ ipython kernel install --user --name=pypsa-earth
    $ jupyter lab


Installation with Docker
====================================
This is an alternative way to create a development environment for PyPSA-Earth. This method is useful for users who are not familiar with programming or Python, or who prefer not to install Python on their local machine. It uses Docker containers to create a development environment for PyPSA-Earth.

This section provides a step-by-step guide on how to set up and use Docker containers to run PyPSA-Earth.

**Steps:**

1. **Install Docker** following the instructions for your operating system:

   * `Windows <https://docs.docker.com/desktop/install/windows-install/>`_
   * `Linux <https://docs.docker.com/desktop/install/linux/>`_
   * `macOS <https://docs.docker.com/desktop/install/mac-install/>`_

.. note::

    Ensure Docker is installed on your system.

2. **Install Visual Studio Code** using `this link <https://code.visualstudio.com/download>`_. Select the most compatible version for your operating system.

3. **Install GitHub Desktop** for your OS using `this link <https://desktop.github.com/download/>`_.

4. **Clone the repository:**

   * Open GitHub Desktop
   * Click on "File" in the top left corner
   * Click on "Clone Repository"
   * Paste the following URL in the URL field:

   .. code:: bash

       https://github.com/pypsa-meets-earth/pypsa-earth.git

   * Click on "Clone"
   * Choose the location where you want to save the repository
   * Click on "Current Branch: main" and select `devContainers`
   * Click on "Open in Visual Studio Code"

   The repository will be cloned to your local machine.

5. **Rebuild and open in a container:**

   * Open the repository in VSCode
   * Click on the icon in the far bottom left corner of the VSCode window
   * Click on "Reopen in Container"
   * Wait for the container to build and open the repository in the container

The environment will be ready for use. You can now run PyPSA-Earth in the container.

===============
Troubleshooting
===============

Common Issues and Solutions
---------------------------

**Environment Creation Fails**
    - Ensure you have sufficient disk space (at least 5 GB for the environment)
    - Try using ``conda`` instead of ``mamba`` if installation fails
    - Check your internet connection and try again

**Java Not Found**
    - Verify Java installation: ``java --version``
    - Ensure Java is in your system PATH
    - Restart your terminal after Java installation

**Snakemake Command Not Found**
    - Make sure the ``pypsa-earth`` environment is activated
    - Run ``conda activate pypsa-earth`` in each new terminal session
    - Verify installation with ``conda list snakemake``

**Git Clone Fails**
    - Ensure the destination path contains no spaces
    - Check your internet connection
    - Try using HTTPS instead of SSH: ``git clone https://github.com/pypsa-meets-earth/pypsa-earth.git``

**Out of Memory Errors**
    - Ensure you have at least 8 GB RAM available
    - Close unnecessary applications
    - Consider using a machine with more RAM for large models

**Platform-Specific Lock File Not Available**
    - Use the generic ``environment.yaml`` file instead
    - Be aware that this may lead to compatibility issues
    - Consider contributing by generating lock files for your platform

Getting Help
------------

If you encounter issues not covered here:

1. Check the `GitHub Issues <https://github.com/pypsa-meets-earth/pypsa-earth/issues>`_ for similar problems
2. Join the `Discord community <https://discord.gg/AnuJBk23FU>`_ for support
3. Consult the :ref:`software_hints` section for additional guidance
