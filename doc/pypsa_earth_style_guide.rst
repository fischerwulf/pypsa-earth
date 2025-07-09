.. SPDX-FileCopyrightText:  PyPSA-Earth and PyPSA-Eur Authors
..
.. SPDX-License-Identifier: CC-BY-4.0

##########################################
PyPSA-Earth Documentation Style Guide
##########################################

Overview
========

This style guide ensures consistency and clarity across all PyPSA-Earth documentation. The goal is to create a quietly authoritative style that focuses on brief, friendly explanations while maintaining technical accuracy. The methodology section should be free from explicit technical details while making the implementation understandable.

Core Style Principles
=====================

**Primary Objectives:**
- Help new users understand concepts without technical implementation details
- Maintain quietly authoritative tone without unnecessary verbosity
- Avoid excessive marketing language
- Focus on conceptual understanding and general methodology approaches
- Ensure technical accuracy while prioritizing accessibility and conceptual clarity

**Target Audience Priority:**
1. New users seeking conceptual understanding
2. Technical users requiring implementation details
3. Advanced users needing reference material

Writing Style and Tone
======================

Voice and Perspective
--------------------

**Use passive/impersonal constructions:**
- ✅ "It is possible to model energy systems at multiple scales"
- ✅ "The framework allows for flexible geographic scoping"
- ✅ "Results can be visualized using the plotting module"
- ❌ "You can model energy systems" (too direct)
- ❌ "We implement advanced algorithms" (too personal)

**Maintain quietly authoritative tone:**
- ✅ "PyPSA-Earth employs a linear programming approach"
- ✅ "The optimization framework ensures computational tractability"
- ❌ "PyPSA-Earth's revolutionary approach transforms energy modeling"
- ❌ "Our cutting-edge methodology provides unparalleled accuracy"

**Focus on capabilities rather than features:**
- ✅ "The model supports multi-scale analysis from local to continental levels"
- ✅ "Automated data processing extracts information from multiple sources"
- ❌ "PyPSA-Earth has amazing multi-scale capabilities"
- ❌ "Our automated data processing feature is incredibly powerful"

Terminology and Abbreviations
=============================

First Mention Protocol
----------------------

**All technical terms and acronyms must be defined at first mention:**

Format: "Full Term (Abbreviation)" or "Full Term (FT)"

**Examples:**
- ✅ "Optimal Power Flow (OPF) algorithms optimize electricity dispatch"
- ✅ "OpenStreetMap (OSM) provides geospatial infrastructure data"
- ✅ "Linear Programming (LP) ensures computational efficiency"
- ✅ "Photovoltaic (PV) generation follows weather patterns"

**Subsequent mentions use abbreviation only:**
- ✅ "The OPF formulation includes transmission constraints"
- ✅ "OSM data undergoes validation before network construction"

**Exception:** Common abbreviations may be used without definition if universally understood in energy context (e.g., MW, GW, kWh)

Standardized Terminology
-----------------------

**Core Terms (use consistently):**
- "energy system" (not "electrical system" or "power system")
- "optimization" (not "optimisation")
- "network topology" (not "grid topology")
- "transmission lines" (not "power lines")
- "renewable energy" (not "renewables" alone)
- "load centers" (not "demand centers")
- "generation capacity" (not "installed capacity")
- "temporal resolution" (not "time resolution")
- "spatial resolution" (not "geographic resolution")

**Technical Process Terms:**
- "data processing" (not "data handling")
- "network reconstruction" (not "network building")
- "workflow management" (not "pipeline management")
- "validation framework" (not "validation system")
- "optimization procedure" (not "optimization process")

Content Structure and Organization
==================================

Information Hierarchy
---------------------

**For Methodology Section Files:**

**1. Conceptual Overview (Always First)**
- Brief explanation of what the method/tool does
- Why it matters for energy system modeling
- High-level workflow description

**2. Implementation Approach (Second)**
- General methodology without technical details
- Key steps and their purpose
- Data requirements and outputs
- Conceptual flow and decision points

**3. Cross-References to Technical Details**
- References to detailed mathematical formulations in appendices
- Links to algorithm specifics in technical documentation
- Pointers to implementation examples in tutorials

**For Non-Methodology Files:**

**1. Conceptual Overview (Always First)**
- Brief explanation of what the method/tool does
- Why it matters for energy system modeling
- High-level workflow description

**2. Implementation Approach (Second)**
- General methodology without technical details
- Key steps and their purpose
- Data requirements and outputs

**3. Technical Details (Separate Section)**
- Mathematical formulations
- Algorithm specifics
- Parameter definitions
- Detailed examples

**Example Structure for Methodology Files:**
```
Section Title
=============

Overview
--------
Brief conceptual explanation...

Implementation Approach
----------------------
General methodology and workflow...

Data Requirements
----------------
Input data and sources...

Cross-References
----------------
Links to technical details in other sections...
```

**Example Structure for Non-Methodology Files:**
```
Section Title
=============

Overview
--------
Brief conceptual explanation...

Implementation
--------------
General approach without technical details...

Technical Details
-----------------
Mathematical formulations and specifics...
```

Technical Detail Separation
---------------------------

**For Methodology Section:**

The methodology section should focus exclusively on conceptual understanding. Technical details should be handled through cross-references:

1. **Use cross-references instead of inline technical details:**
   - "For mathematical formulation details, see :ref:`mathematical_appendix`"
   - "Algorithm specifics are provided in :ref:`technical_reference`"
   - "Implementation examples are available in :ref:`tutorial_section`"

2. **Maintain conceptual focus:**
   - Explain what the method does and why
   - Describe the general approach without formulas
   - Focus on methodology flow and decision points
   - Avoid mathematical notation in methodology sections

3. **Reserve technical content for dedicated sections:**
   - Mathematical frameworks in appendices
   - Algorithm details in technical reference
   - Implementation specifics in tutorials

**For Non-Methodology Files:**

Technical content can be included but should be clearly separated:

1. **Separate subsections with clear headers:**
   - "Technical Details"
   - "Mathematical Formulation"
   - "Algorithm Specifics"
   - "Advanced Configuration"

2. **Use admonitions for technical notes:**
   ```
   .. note::
      Technical Detail: The optimization uses mixed-integer linear programming
      when binary variables are required for unit commitment decisions.
   ```

3. **Reference detailed explanations:**
   - "For mathematical formulation details, see :ref:`mathematical_framework`"
   - "Algorithm specifics are provided in :ref:`technical_appendix`"

Mathematical Notation
=====================

Formatting Standards
-------------------

**Variables:**
- Scalars: italic (*p*, *q*, *c*)
- Vectors: bold (**x**, **y**, **z**)
- Matrices: bold uppercase (**A**, **B**, **C**)
- Sets: calligraphic or bold uppercase (**N**, **L**, **G**)

**Indices:**
- Subscripts: *i*, *j*, *k* for nodes/locations
- Time indices: *t* for time periods
- Technology indices: *r* for generators, *s* for storage
- Line indices: *l* for transmission lines

**Equation Formatting:**
- Use numbered equations: `.. math::` directive
- Include variable definitions after each equation
- Reference format: "as shown in equation (1)" or "see equation (1)"

**Example:**
```
.. math::
    \min_{G,H,F,g,h,e} AC = \sum_{i,r} (c_{i,r} \cdot G_{i,r}) + \sum_{l} (c_l \cdot F_l)

where:
- :math:`G_{i,r}` = generation capacity of technology *r* at location *i*
- :math:`c_{i,r}` = capacity-related investment costs
- :math:`F_l` = transmission line capacity for line *l*
```

Section Structure Standards
==========================

Heading Hierarchy
-----------------

**Standard heading levels:**
```
##########################################
Document Title (H1)
##########################################

Section Title (H2)
==================

Subsection Title (H3)
---------------------

Sub-subsection Title (H4)
^^^^^^^^^^^^^^^^^^^^^^^^^

Paragraph Title (H5)
""""""""""""""""""""
```

**Usage guidelines:**
- H1: Document title only
- H2: Major sections (Overview, Implementation, Technical Details)
- H3: Subsections within major sections
- H4: Detailed breakdowns
- H5: Rare use for very specific topics

Standard Section Templates
--------------------------

**For Methodology Files:**
```
Overview
========
Brief conceptual explanation of the methodology...

Implementation Approach
======================
General description of how the method works...

Data Requirements
================
Input data and sources...

Cross-References
===============
Links to technical details in other documentation sections...
```

**For Non-Methodology Files:**
```
Overview
========
Brief conceptual explanation of the methodology...

Implementation Approach
======================
General description of how the method works...

Data Requirements
================
Input data and sources...

Technical Details
================
Mathematical formulations and algorithm specifics...

Validation and Quality Control
=============================
How accuracy is ensured...
```

**For Tutorial Files:**
```
Introduction
============
What this tutorial covers...

Prerequisites
=============
Required knowledge and setup...

Step-by-Step Guide
==================
Implementation steps...

Advanced Options
===============
Optional technical details...

Troubleshooting
===============
Common issues and solutions...
```

Code Examples and Formatting
============================

Code Block Standards
--------------------

**Python code formatting:**
```python
# Brief comment explaining the code block purpose
import pypsa
import pandas as pd

# Create network object
network = pypsa.Network()

# Add components with clear parameter names
network.add("Bus", "regional_bus", 
           x=longitude, y=latitude, 
           country="example_country")
```

**Configuration file examples:**
```yaml
# Configuration section description
solving:
  solver:
    name: gurobi
    options:
      method: 2
      threads: 4
```

**Comment guidelines:**
- Use English for all comments
- Explain purpose, not obvious syntax
- Include units where relevant
- Reference related documentation sections

Cross-References and Navigation
==============================

Reference Formatting
--------------------

**Internal references:**
- ✅ "For detailed mathematical formulation, see :ref:`mathematical_framework`"
- ✅ "The data processing methodology is described in :ref:`data_processing`"
- ❌ "See the mathematical framework section for details"

**External references:**
- ✅ "PyPSA framework documentation (https://pypsa.readthedocs.io/)"
- ✅ "OpenStreetMap data model (OSM Wiki, 2024)"

**Figure and table references:**
- ✅ "Figure 1 shows the network topology"
- ✅ "Table 2 summarizes the data sources"

Navigation Principles
--------------------

**Information progression:**
1. Conceptual understanding first
2. Implementation overview second
3. Technical details available but separate
4. Cross-references for deeper exploration

**Link strategy:**
- Provide context for links ("For implementation details, see...")
- Use descriptive link text, not "click here"
- Balance detail depth with accessibility

Quality Assurance Checklist
===========================

**Before publishing any documentation:**

**Content Review:**
- [ ] Conceptual explanation comes before implementation details
- [ ] All acronyms defined at first mention
- [ ] Terminology matches style guide standards
- [ ] For methodology files: No technical details included, only cross-references
- [ ] For non-methodology files: Technical details separated from overview
- [ ] Implementation approach clearly explained

**Style Consistency:**
- [ ] Quietly authoritative tone maintained
- [ ] No unnecessary verbosity or marketing language
- [ ] Impersonal voice used throughout
- [ ] Mathematical notation follows standards
- [ ] Heading hierarchy correct

**Technical Accuracy:**
- [ ] Mathematical formulations validated
- [ ] Code examples tested and functional
- [ ] Cross-references verified
- [ ] External links working
- [ ] Figures and tables properly referenced

**User Experience:**
- [ ] New users can understand concepts without technical details
- [ ] Methodology sections focus on conceptual understanding
- [ ] Technical users can find implementation specifics through cross-references
- [ ] Navigation flow supports different user needs
- [ ] Information density appropriate for section purpose

Implementation Notes
====================

**Applying this style guide:**

1. **Review existing content** against style principles
2. **Identify sections** that mix concepts with technical details
3. **For methodology files**: Remove technical details and replace with cross-references
4. **For non-methodology files**: Restructure content to separate overview from implementation
5. **Standardize terminology** throughout all files
6. **Validate conceptual accuracy** after style changes
7. **Test user journey** from basic to advanced content through cross-references

**Priority order:**
1. Methodology section (highest impact)
2. Introduction and index pages
3. Tutorial and configuration files
4. Reference documentation

This style guide ensures PyPSA-Earth documentation maintains consistency while serving users at different technical levels effectively. The methodology section focuses on conceptual understanding, while technical details are available through cross-references to appropriate sections.
