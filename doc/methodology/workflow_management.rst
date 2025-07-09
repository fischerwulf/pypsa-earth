.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _workflow_management:

##########################################
Workflow Management
##########################################

Overview
========

PyPSA-Earth relies on Snakemake workflow management to decompose complex energy system modeling into automated, reproducible, and transparent processes. This section documents the workflow architecture, design principles, and implementation strategies that enable scalable and maintainable modeling workflows.

Snakemake Workflow Architecture
===============================

Rule-Based Task Decomposition
-----------------------------

PyPSA-Earth implements a sophisticated rule-based workflow architecture using Snakemake, where complex energy system modeling tasks are decomposed into individual, manageable rules. Each rule defines:

* **Input/Output specifications**: Clear data dependencies and expected outputs
* **Script execution**: Python scripts that perform specific modeling tasks
* **Resource requirements**: Memory, CPU, and time constraints for optimal execution
* **Conditional execution**: Rules that execute only when specific conditions are met

Key rule categories in PyPSA-Earth include:

* **Data retrieval rules**: `retrieve_databundle_light`, `download_osm_data`
* **Network building rules**: `build_osm_network`, `base_network`, `build_shapes`
* **Data processing rules**: `build_demand_profiles`, `build_renewable_profiles`
* **Model preparation rules**: `add_electricity`, `simplify_network`, `cluster_network`
* **Analysis rules**: `solve_network`, `make_summary`, `plot_summary`

Dependency Management
--------------------

Snakemake's dependency management ensures that:

1. **Automatic dependency resolution**: Rules execute in the correct order based on input/output dependencies
2. **Incremental updates**: Only rules with changed inputs or missing outputs are re-executed
3. **Parallel execution**: Independent rules can run simultaneously to optimize computational efficiency
4. **Error propagation**: Failed rules prevent dependent rules from executing, maintaining data integrity

The workflow automatically handles complex dependencies such as:

- Geographic data processing before network construction
- Weather data preparation before renewable profile generation  
- Network simplification before optimization
- Result generation before plotting and summarization

Automatic Chaining
------------------

PyPSA-Earth's workflow architecture enables seamless chaining of modeling processes through:

* **Wildcard expansion**: Automatic generation of multiple scenarios, countries, or time periods
* **Configuration-driven execution**: YAML configuration files control which rules execute
* **Dynamic rule selection**: Conditional rule inclusion based on enabled features
* **Target-driven execution**: Users specify end goals, and Snakemake determines required intermediate steps

Example workflow chains:

- `countries → osm_data → network → demand → renewables → electricity → optimization → results`
- `cutout → weather_data → capacity_factors → generation_profiles → network_model`

Reproducibility and Transparency
===============================

Modular Design Principles
-------------------------

PyPSA-Earth's modular workflow design promotes:

**Separation of Concerns**: Each rule focuses on a single, well-defined task:

- Data retrieval is separated from data processing
- Network construction is independent of demand modeling
- Optimization is decoupled from result analysis

**Configurable Execution**: The workflow adapts to different use cases through:

- `config.yaml` files that control rule behavior
- Feature flags (e.g., `enable.build_cutout`, `enable.download_osm_data`)
- Scenario definitions with multiple planning horizons and technology options
- Custom rule integration for specialized analyses

**Reusable Components**: Workflow modules can be:

- Applied to different geographic regions
- Executed with varying temporal resolutions
- Scaled from single countries to continental analyses
- Extended with custom rules for specific research questions

Version Control Integration
--------------------------

The workflow maintains reproducibility through:

* **Git integration**: Automatic tracking of commit hashes in configuration
* **Environment specification**: Conda environment files ensure consistent dependencies
* **Configuration versioning**: Config file version checks prevent compatibility issues
* **Provenance tracking**: Each model run records the exact code version and parameters used

Documentation and Provenance
----------------------------

PyPSA-Earth maintains comprehensive workflow documentation through:

* **Automatic logging**: Detailed logs of rule execution, timing, and resource usage
* **Configuration recording**: Complete parameter sets saved with each model run
* **Intermediate file preservation**: Key intermediate outputs saved for inspection and debugging
* **Result summarization**: Automated generation of summary statistics and validation metrics

User Experience Improvements
============================

Automated Model Building
------------------------

PyPSA-Earth's automated workflow eliminates manual intervention in model construction:

**One-Command Execution**: Users can generate complete energy system models with a single Snakemake command:

- `snakemake solve_all_networks` - Complete workflow from data to results
- `snakemake plot_all_summaries` - Full analysis including visualization
- `snakemake make_all_summaries` - Comprehensive result summarization

**Configuration-Driven Customization**: Model characteristics are controlled through YAML files:

- Geographic scope (single countries to continental regions)
- Temporal resolution (hourly to seasonal aggregation)
- Technology options and cost assumptions
- Network clustering and simplification levels
- Scenario definitions for policy analysis

**Intelligent Caching**: The workflow optimizes computation time through:

- Automatic detection of completed intermediate steps
- Shared resource utilization across multiple model runs
- Incremental updates when only configuration changes
- Optional reuse of computationally expensive steps (e.g., weather data processing)

Workflow Visualization
---------------------

Snakemake provides powerful visualization capabilities for PyPSA-Earth workflows:

**Dependency Graphs**: Visual representation of rule relationships and data flow:

- `snakemake --dag | dot -Tpng > workflow.png` - Complete workflow visualization
- `snakemake --rulegraph | dot -Tpng > rules.png` - Rule-level dependency graph

**Execution Monitoring**: Real-time tracking of workflow progress:

- Progress bars for long-running operations
- Resource usage monitoring and reporting
- Execution time profiling for performance optimization
- Detailed logging with configurable verbosity levels

**Result Dashboards**: Automated generation of summary visualizations and reports

Error Handling and Debugging
----------------------------

PyPSA-Earth implements robust error handling and debugging capabilities:

**Graceful Failure Management**: 

- Optional scenario failure tolerance with `allow_scenario_failure`
- Detailed error reporting with context information
- Automatic cleanup of partial outputs on rule failure
- Restart capability from failed rules without full re-execution

**Debugging Support**:

- Dry-run mode to validate workflow without execution
- Detailed logging with rule-specific information
- Intermediate file inspection for troubleshooting
- Configuration validation and version checking

**Quality Assurance**:

- Automatic validation of input data formats and ranges
- Consistency checks across different data sources
- Warning systems for potential modeling issues
- Built-in data quality metrics and reporting

Performance Optimization
========================

Parallelization Strategies
--------------------------

PyPSA-Earth leverages Snakemake's parallelization capabilities for computational efficiency:

**Rule-Level Parallelization**: Independent rules execute simultaneously:

- Multiple country data downloads run in parallel
- Renewable profiles for different technologies computed concurrently  
- Independent scenario optimizations executed simultaneously
- Geographic region processing parallelized across available cores

**Internal Task Parallelization**: Individual rules utilize multi-threading:

- OpenStreetMap data processing with configurable thread counts
- Weather data extraction optimized for parallel I/O
- Network clustering algorithms with parallel implementations
- Matrix operations in optimization leveraging BLAS libraries

**Scenario Parallelization**: Multiple scenarios processed simultaneously:

- Different planning horizons (2030, 2040, 2050)
- Various technology cost assumptions
- Monte Carlo uncertainty analysis iterations
- Policy scenario comparisons

Resource Management
------------------

Efficient resource utilization through:

**Memory Management**:

- Automatic memory requirement estimation for rules
- Configurable memory limits to prevent system overload
- Memory-efficient data structures for large geographic datasets
- Garbage collection optimization for long-running workflows

**CPU Optimization**:

- Intelligent core allocation based on rule characteristics
- NUMA-aware processing for multi-socket systems
- Processor affinity configuration for compute-intensive tasks
- Dynamic load balancing across available resources

**Storage Management**:

- Temporary file cleanup to manage disk space
- Configurable output retention policies
- Compression for intermediate large datasets
- Optional cloud storage integration for distributed computing

HPC Integration
==============

High-Performance Computing
--------------------------

PyPSA-Earth supports HPC environments through Snakemake's cluster integration:

**Cluster Scheduler Integration**:

- SLURM workload manager support for large computing clusters
- PBS/Torque compatibility for traditional HPC systems
- LSF integration for enterprise computing environments
- Cloud computing platform support (AWS, Google Cloud, Azure)

**Resource Specification**:

- Per-rule resource requirements (CPU cores, memory, walltime)
- Queue selection based on computational requirements
- GPU utilization for specialized optimization algorithms
- Storage requirements and scratch space management

**Scalability Features**:

- Linear scaling from single nodes to thousand-core clusters
- Efficient job submission and monitoring
- Automatic retry mechanisms for transient cluster issues
- Dynamic resource allocation based on workload characteristics

Cluster Management
-----------------

Advanced cluster management capabilities include:

**Job Scheduling Optimization**:

- Intelligent batching of small tasks to reduce scheduler overhead
- Priority-based execution for time-critical analyses
- Resource pooling across multiple cluster partitions
- Cost optimization for cloud-based computing

**Fault Tolerance**:

- Automatic resubmission of failed jobs
- Checkpointing for long-running optimizations
- Graceful handling of node failures and network interruptions
- State recovery mechanisms for workflow resumption

**Monitoring and Reporting**:

- Real-time cluster resource utilization tracking
- Job performance profiling and bottleneck identification
- Cost tracking and budget management for cloud deployments
- Automated reporting of computational efficiency metrics

References
==========

For related information, see:

* :doc:`data_processing` - Data processing workflows
* :doc:`validation_framework` - Quality assurance workflows
* :doc:`../tutorial_electricity` - Practical workflow examples
