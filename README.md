<script src="./node_modules/markdown-it-asciimath/ASCIIMathTeXImg.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.css">

# CMIP5_patterns
This repository contains a library of temperature and precipitation patterns generated by a least squared regression for all available CMIP5 models. 

###**Pattern scaling:**

Coordinated climate model experiments are bound by a limited number of possible forcing scenarios, which makes exploring uncertainties in climate projections difficult. In the absence of a large sample of model experiments to draw upon, extrapolation outside of the range of projections, as well as interpolation between scenarios can be used to reduce uncertainty from future forcing by spanning a much larger range of emission scenarios.  One such computationally efficient method to explore many different future forcing scenarios scaled from general circulation models (GCMs) is called 'pattern scaling' (Santer, 1990; Mitchell et al, 1999). 

Under the assumption that a climate variable scales propotionally with global mean temperature change, a "pattern" (the statistical relationship between a climate variable and global mean temperature) can be derived from any GCM.
Those patterns can then be "scaled" by a global temperature change obtained from a simple climate model (SCM) to span a wide range of future scenarios that may not have been simulated by full GCMs.

![](https://github.com/JGCRI/CMIP5_patterns/blob/master/IMAGES/FLOWCHART_PS.png)

###**Pattern generation**:

The least squared regression (LSR) patterns are calculated from future forcing scenarios only.  

####**LSR equation**:
[//]: # (var md = require('markdown-it')();)

[//]: # (md.use(require("./node_modules/markdown-it-asciimath/index.js"));)


*TL* = \alpha + \beta * *TG* + \epsilon


*TG* is the global mean surface temperature time series (one-dimensional, unsmoothed), and *TL* is the gridded time series (three dimensional).  $\beta$  is a two-dimensional field of regression slopes, and $\epsilon$ is a two-dimensional residual term (error) stemming from linearly fitting the dependent variable to the predictor.  $\alpha$ is the $y$-intercept, which we take to be 0 by only computing change, not absolute temperature. 

####**Pattern metatdata**

The purpose of creating this pattern library was to allow for researchers across various fields to be able to efficiently use the statistical patterns generated by the described regression method to examine model response to change in global mean temperature for all the available CMIP5 models.  We also further intend for those patterns to be easy to scale using a scaler generated from a SCM of ones choosing.  To this end, included in each netcdf file is:

1.  The individual model pattern (2-D);

2.  The adjusted R^2 between the predictor and dependent terms (2-D); 

3.  The regression error term (2-D);

  *which can be used to construct a residual time series

4.  A historical climatology based on the 1960-1999 average (2-D); 

  *which can be used to construct absolute values at time X 

5.  The 95th percentile confidence level pattern. 

  *which can be used to calculate the 95th and 5th confidence intervals

All source code used to produce these patterns is found [here](https://github.com/JGCRI/CMIP5_patterns/tree/master/SRC). Individual temperature and precipitation patterns in a .nc file are found [here](https://github.com/JGCRI/CMIP5_patterns/tree/master/DATA).

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.235905.svg)](https://doi.org/10.5281/zenodo.235905)

###**References**:

TBA

This work is supported by the [Integrated Assessment Research Program](http://science.energy.gov/ber/research/cesd/integrated-assessment-of-global-climate-change/) of the Office of Science, U.S. Department of Energy. The Pacific Northwest National Laboratory is operated for DOE by Battelle Memorial Institute under contract DE-AC05-76RL01830.
