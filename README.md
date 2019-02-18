The complete documentation of VSpal is under construction at [its home page](https://github.com/accarniel/SpatialPlateauAlgebra).

To cite the Vague Spatial Data Library (VSpal), please mention its conceptual paper:

* [Carniel, A. C.; Schneider, M. Spatial Plateau Algebra: An Executable Type System for Fuzzy Spatial Data Types. In Proceedings of the 2018 IEEE International Conference on Fuzzy Systems (FUZZ-IEEE 2018), p. 1-8, 2018.](https://ieeexplore.ieee.org/document/8491565)

## NEWS

* [a library in R for creating fuzzy region objects as plateau region objects from real data sets](https://github.com/accarniel/SpatialPlateauAlgebra/building_fuzzy_regions/building_plateau_regions).

## Overview

VSpal (short for *Vague Spatial Data Library*) is a C library with the following goal: to provide a common environment for manipulating vague spatial data based on distinct representating models, such as exact models and fuzzy set theory. We are working on making VSpal publicly available. It will 

* provide support for vague spatial data types and their operations based on the [Vague Spatial Algebra](https://www.sciencedirect.com/science/article/pii/S0306437909000519). Currently, there is one implementation based on this algebra, called [VagueGeometry](https://seer.ufmg.br/index.php/jidm/article/view/1367/2645). Our intention is to provide the underlying implementation of VagueGeometry into VSPal.
* provide support for plateau spatial data types and their operations based on the [Plateau Spatial Algebra](https://ieeexplore.ieee.org/document/8491565). This algebra defines an implementation concept for fuzzy spatial data types and their operations reusing exiting implementations of crisp spatial algebras.
* provide support for fuzzy spatial data types and their operations based on the [Fuzzy Spatial Algebra](https://ieeexplore.ieee.org/document/7737976). This is a future work that we are currently working on.

## What are vague (fuzzy) spatial objects?

Current spatial database systems and GIS almost exclusively process *crisp* spatial objects. These are characterized by precisely determined, exact, and homogeneous geometries in the Euclidean plane and have been standardized by means of *spatial data types* for two-dimensional point, line, and region objects. The assumption of crisp boundaries and homogeneous interiors of spatial objects harmonizes very well with their internal representation and processing in a computer favoring precise and unique data structures. Examples of spatial objects are the locations of hydrants, power poles, traffic signs, and ATMs represented as crisp point objects, the routes of highways, streets, guardrails, and rivers modeled as crisp line objects, and the extents of countries, cities, districts, buildings, houses, and airports shaped as crisp region objects. 

While man-made spatial objects nicely accommodate with their modeling as crisp entities, many natural, social, and scientific phenomena reveal an inherently imprecise, blurred, vague, and fuzzy nature but have so far been artificially pressed into a crisp representation and modeling scheme. Geoscientists have shown the need of and their interest in representing spatial vagueness (fuzziness) due to the inadequacy of crisp modeling techniques. 

Spatial fuzziness captures the property of many spatial objects in reality that reveal an intrinsically vague or blurred nature and feature indeterminate boundaries and/or interiors; we call such entities *vague (fuzzy) spatial objects*. A spatial object is fuzzy if locations exist that cannot be assigned completely to the object or to its complement. Examples are natural, social, and cultural phenomena like land features with continuously changing properties (e.g., population density, soil strata, soil quality, vegetation, pollution, temperature, air pressure), lakes, oceans, deserts, and English speaking areas. As another example, the transition between a valley and a mountain cannot be exactly ascertained since it is smooth and seamless and both objects are hence not crisp.

## Features

Currently, VSpal provides a first version of the implementation of the Vague Spatial Algebra.

In addition, it provides a method for creating fuzzy region objects as plateau region objects from real data sets. This method is implemented in R and available [here](https://github.com/accarniel/SpatialPlateauAlgebra/building_fuzzy_regions/building_plateau_regions).
