.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

.. _mathematical_framework:

##########################################
Mathematical Framework
##########################################

Overview
========

PyPSA-Earth employs a linear programming approach for energy system optimization, building on the proven PyPSA framework. This section details the mathematical formulations, optimization objectives, and constraint structures that form the foundation of PyPSA-Earth's modeling capabilities.

Core Mathematical Formulation
=============================

PyPSA-Earth minimizes the total Annualized Costs (AC) of the energy system, comprised of annualized capital and operational expenditures. The objective function is formulated as:

.. math::

    \min_{G,H,F,g,h,e} AC = \left[\sum_{i,r} (c_{i,r} \cdot G_{i,r}) + \sum_{l} (c_l \cdot F_l)\right.
    
    \left.+ \sum_{i,s} (c^{store}_{i,s} \cdot H^{store}_{i,s} + c^-_{i,s} \cdot H^-_{i,s} + c^+_{i,s} \cdot H^+_{i,s})\right.
    
    \left.+ \sum_{i,r,t} (o_{i,r} \cdot g_{i,r,t} \cdot w_t) + \sum_{i,s,t} ((o^+_{i,s} \cdot h^+_{i,s,t} + o^-_{i,s} \cdot h^-_{i,s,t}) \cdot w_t)\right.
    
    \left.+ \sum_{i,s,t} (o^{store}_{i,s} \cdot e_{i,s,t} \cdot w_t)\right]

where:

**Capital Expenditures:**
- :math:`c_{i,r}` = capacity-related investment costs for generator :math:`G_{i,r}` of technology :math:`r` at location :math:`i`
- :math:`c^{store}_{i,s}` = investment costs for storage energy capacity :math:`H^{store}_{i,s}` of technology :math:`s`
- :math:`c^+_{i,s}`, :math:`c^-_{i,s}` = investment costs for charging/discharging capacity :math:`H^+_{i,s}`, :math:`H^-_{i,s}`
- :math:`c_l` = investment costs for transmission line :math:`F_l`

**Operational Expenditures:**
- :math:`o_{i,r}` = variable operational costs for generation :math:`g_{i,r,t}`
- :math:`o^+_{i,s}`, :math:`o^-_{i,s}` = variable costs for storage charging/discharging :math:`h^+_{i,s,t}`, :math:`h^-_{i,s,t}`
- :math:`o^{store}_{i,s}` = energy-level related storage costs :math:`e_{i,s,t}`
- :math:`w_t` = time step duration weights where :math:`\sum^T_{t=1} w_t = 8760` hours

System Constraints
==================

The objective function is subject to multiple linear constraints that ensure realistic system operation and planning. These constraints form a convex linear program with continuous variables, ensuring unique objective values and computational tractability.

Energy Balance and Power Flow Constraints
-----------------------------------------

**Kirchhoff's Current Law (Energy Balance)**

The fundamental energy balance constraint ensures that supply equals demand at each network node:

.. math::

    \sum_r g_{i,r,t} - \sum_s h^+_{i,s,t} + \sum_s h^-_{i,s,t} + \sum_l K_{i,l} \cdot f_{l,t} = d_{i,t} \quad \forall i,t

where:
- :math:`g_{i,r,t}` = generation from technology :math:`r` at node :math:`i` and time :math:`t`
- :math:`h^+_{i,s,t}`, :math:`h^-_{i,s,t}` = storage charging/discharging at node :math:`i`
- :math:`K_{i,l}` = network incidence matrix relating nodes :math:`i` to lines :math:`l`
- :math:`f_{l,t}` = power flow in transmission line :math:`l`
- :math:`d_{i,t}` = inelastic electricity demand at node :math:`i`

**Kirchhoff's Voltage Law (AC Power Flow)**

For AC transmission lines, voltage angle differences around closed cycles must sum to zero:

.. math::

    \sum_l C_{l,c} \cdot x_l \cdot f_{l,t} = 0 \quad \forall c,t

where:
- :math:`C_{l,c}` = cycle basis matrix representing independent cycles :math:`c`
- :math:`x_l` = series inductive reactance of line :math:`l`

This linearized power flow formulation assumes reactance dominates resistance and small voltage angle differences.

Capacity Constraints
-------------------

**Generator Capacity Limits**

.. math::

    \underline{G}_{i,r} \leq G_{i,r} \leq \overline{G}_{i,r} \quad \forall i,r

**Storage Capacity Limits**

.. math::

    \underline{H}_{i,s} \leq H_{i,s} \leq \overline{H}_{i,s} \quad \forall i,s

**Transmission Capacity Limits**

.. math::

    \underline{F}_l \leq F_l \leq \overline{F}_l \quad \forall l

Operational Constraints
----------------------

**Renewable Generation Limits**

For renewable generators (subset :math:`RG`), operation is limited by weather-dependent availability:

.. math::

    0 \leq g_{i,r,t} \leq \bar{g}_{i,r,t} \cdot G_{i,r} \quad \forall i, r \in RG, t

where :math:`\bar{g}_{i,r,t}` represents the normalized availability factor from weather data.

**Transmission Flow Limits**

.. math::

    0 \leq f_{l,t} \leq \bar{f}_{l,t} \cdot F_l \quad \forall l,t

Storage System Constraints
-------------------------

**Storage Charging/Discharging Limits**

.. math::

    0 \leq h^+_{i,s,t} \leq H^+_{i,s} \quad \forall i,s,t

.. math::

    0 \leq h^-_{i,s,t} \leq H^-_{i,s} \quad \forall i,s,t

**Storage Energy Balance**

The storage energy level evolution accounts for charging, discharging, natural inflow, spillage, and standing losses:

.. math::

    e_{i,s,t} = \eta_{i,s,+} \cdot e_{i,s,t-1} + \eta_{i,s,+} \cdot w_t \cdot h^+_{i,s,t} - \eta^{-1}_{i,s,-} \cdot w_t \cdot h^-_{i,s,t}
    
    + w_t \cdot h^{inflow}_{i,s,t} - w_t \cdot h^{spillage}_{i,s,t} \quad \forall i,s,t

where:
- :math:`\eta_{i,s,+}`, :math:`\eta_{i,s,-}` = charging/discharging efficiencies
- :math:`h^{inflow}_{i,s,t}` = natural inflow (e.g., hydro reservoirs)
- :math:`h^{spillage}_{i,s,t}` = spillage losses

**Storage Energy Capacity Limits**

.. math::

    0 \leq e_{i,s,t} \leq H^{store}_{i,s} \quad \forall i,s,t

**Technology-Specific Energy-to-Power Ratio**

.. math::

    0 \leq e_{i,s,t} \leq T^s \cdot H^-_{i,s} \quad \forall i,s,t

where :math:`T^s` defines the energy-to-discharging power ratio for storage technology :math:`s`.

**Cyclic Storage Operation**

Storage units must operate cyclically over the optimization period:

.. math::

    e_{i,s,0} = e_{i,s,T} \quad \forall i,s

Environmental Constraints
------------------------

**Greenhouse Gas Emissions Limit**

Total system emissions can be constrained by:

.. math::

    \sum_{i,r,t} g_{i,r,t} \cdot \gamma_r \leq GHG

where:
- :math:`\gamma_r` = emission intensity of technology :math:`r`
- :math:`GHG` = total emissions limit

Linear Programming Approach
===========================

PyPSA-Earth employs linear programming (LP) to solve the energy system optimization problem. The mathematical formulation ensures:

**Convexity and Optimality**
    The linear objective function and constraints create a convex feasible region, guaranteeing a unique optimal objective value. While multiple optimal solutions may exist operationally, the cost-optimal solution is unique.

**Computational Tractability**
    Linear formulation enables efficient solution of large-scale problems using established LP solvers, though complex scenarios may require multiple days of computation time.

**Modeling Assumptions**
    Key linearization assumptions include:
    
    * DC power flow approximation (reactance >> resistance)
    * Small voltage angle differences
    * Linear cost functions
    * Piecewise linear approximations for non-linear relationships

Multi-Year Optimization Formulations
====================================

PyPSA-Earth supports multi-year investment planning through extended temporal formulations:

**Investment Periods**
    The model can optimize investments across multiple planning periods, typically representing years or decades.

**Annualization Approach**
    Capital costs are annualized using technology-specific discount rates and lifetimes to enable consistent comparison across time periods.

**Dynamic Constraints**
    Multi-year formulations can include:
    
    * Technology learning curves
    * Resource depletion constraints  
    * Cumulative emission budgets
    * Infrastructure depreciation

Investment and Operational Integration
=====================================

The optimization simultaneously determines:

**Capacity Investment Decisions**
    * Generator capacities :math:`G_{i,r}`
    * Storage capacities :math:`H_{i,s}` (energy and power)
    * Transmission line capacities :math:`F_l`

**Operational Dispatch**
    * Hourly generation schedules :math:`g_{i,r,t}`
    * Storage operation :math:`h^+_{i,s,t}`, :math:`h^-_{i,s,t}`
    * Power flows :math:`f_{l,t}`

This integrated approach ensures investment decisions account for operational constraints and costs, leading to more realistic and economically efficient solutions.

Sector Coupling Mathematical Representations
============================================

PyPSA-Earth extends the core electricity model to include sector coupling:

**Heat Sector Integration**
    * Heat pumps and resistance heaters linking electricity and heating
    * District heating networks with thermal storage
    * Combined heat and power (CHP) units

**Transport Sector Integration**
    * Electric vehicle charging profiles
    * Synthetic fuel production pathways
    * Transport demand electrification

**Industrial Sector Integration**
    * Power-to-X processes (hydrogen, ammonia, steel)
    * Industrial heat demand and supply
    * Process electrification pathways

These sectors are modeled through additional nodes, links, and constraints that extend the core electricity formulation.

Uncertainty Handling in Optimization
====================================

PyPSA-Earth provides several approaches for handling uncertainty:

**Deterministic Scenarios**
    Multiple scenarios with different input assumptions to explore sensitivity to key parameters.

**Stochastic Programming**
    Probabilistic formulations that explicitly model uncertainty in renewable resources, demand, and costs.

**Robust Optimization**
    Solutions that perform well across multiple uncertainty realizations without requiring probability distributions.

Solution Properties and Convergence
===================================

**Existence and Uniqueness**
    The linear programming formulation guarantees solution existence when the feasible region is non-empty and bounded. The optimal objective value is unique, though multiple optimal solutions may exist.

**Convergence Criteria**
    Standard LP convergence criteria include:
    
    * Primal and dual feasibility tolerances
    * Optimality gap thresholds
    * Maximum iteration limits

**Numerical Considerations**
    Large-scale energy system models may face numerical challenges:
    
    * Matrix conditioning and scaling
    * Variable bound management
    * Constraint coefficient ranges
    * Solver-specific parameter tuning

The PyPSA framework provides robust default settings while allowing advanced users to customize solver parameters for specific applications.

References
==========

For implementation details, see:

* :doc:`network_modeling` - Network topology constraints
* :doc:`data_processing` - Data preparation for optimization
* :doc:`validation_framework` - Solution validation methods
