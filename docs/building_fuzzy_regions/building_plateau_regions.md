# Constructing Plateau Region Objects from Real Data Sets

## Overview

Here, we provide a systematic and generic approach to the general issue of collecting and constructing fuzzy region objects as plateau region objects from real data sets and leveraging domain expert knowledge. This method is implemented as R functions. Given a set of crisp points, each of which is assigned some kind of alphanumerical value of a given application context, we show with the aid of domain expert knowledge how to extract plateau regions that represent different nuances of the data set. This two-stage extraction method provides a flexible algorithm for users and enables the user employs the most appropriate policies for a given application situation. The two stages of our method are:

* [Fuzzification Stage](#fuzzification_stage)
* [Construction Stage](#construction_stage)

## Fuzzification Stage

This stage consists of the application of well-known techniques from fuzzy set theory to assign membership degrees to each point of a given point data set. Hence, the technique to be employed is a parameter of this stage in the form of a **fuzzification policy**. In our implementation, we provide the following policies:

* [Fuzzy Set Policy](#fuzzy_set_policy)
* [Fuzzy Clustering Policy](#fuzzy_clustering_policy)
* [Fuzzy Classification Policy](#fuzzy_classification_policy)

### Fuzzy Set Policy

This policy is implemented by the function *fuzzysetpolicy*, which has the following required parameters:

* **data**: It is a data frame composed of three columns, *x*, *y*, and *z*. The columns *x* and *y* defines the point of the geographical location, whereas *z* specifies the numerical value associated to the point.
* **classes**: It is a list of strings containing the name of the classes in which the points may represent. That is, what are the possible representations that the fuzzy phenomenon can assume. Each class represents a fuzzy set in **fuzzysets**. For instance, the class in the position 0, represents the fuzzy set in the position 0 in **fuzzysets**.
* **fuzzysets**: It is a list of fuzzy sets represented as fuzzy numbers. The fuzzy number is represented by the R package [FuzzyNumbers](https://cran.r-project.org/web/packages/FuzzyNumbers/vignettes/FuzzyNumbersTutorial.pdf). Each fuzzy set represents a possible characterization (class) of the fuzzy phenomenon and its meanings is identified by a corresponding entry in **classes**.

This policy returns a data frame containing the following columns: 

* *x* and *y* are the same points from the **data**.
* *i* columns of numerical values, where *i* is the number of classes contained in **fuzzysets** and **classes**. The name of these columns are the names contained in **classes**. Each column has the membership point of (*x*, *y*) at the corresponding fuzzy number representing the class.

### Fuzzy Clustering Policy

This policy is implemented by the function *fuzzyclusteringpolicy*, which has the following required parameters:

* **data**: It is a data frame composed of three columns, *x*, *y*, and *z*. The columns *x* and *y* defines the point of the geographical location, whereas *z* specifies the numerical value associated to the point.
* **method**: It defines the fuzzy clustering algorithm to be employed in the policy. Currently, it can only assume the following values: (i) *cmeans*, which specifies the use of the [fuzzy c-means](https://www.sciencedirect.com/science/article/pii/0098300484900207), and (ii) *cshell*, which specifies the use of the [fuzzy c-shell](https://www.tandfonline.com/doi/abs/10.1080/03081079008935087). These methods are implemented by the R package [e1071](https://cran.r-project.org/web/packages/e1071/e1071.pdf).
* **sclus**: It is a Boolean value that specifies whether the coordinates *x* and *y* are also used by the fuzzy clustering algorithm (*true*) or not (*false*).
* **k**: It specifies the number of groups to be created.
* **iter**: The number of iterations to be processed by the fuzzy clustering algorithm.

This policy returns a data frame containing the following columns: 

* *x* and *y* are the same points from the **data**.
* *k* columns of numerical values, where *k* is the number of groups specifies when executing the policy. The user should analyze the returning data in order to specify the meaning of each group.

### Fuzzy Classification Policy

*To be specified.*

## Construction Stage

The construction stage integrates the result obtained by the execution of the fuzzification stage with the application of spatial algorithms to group points with similar characteristics. This integration leads to the creation of plateau region objects. In our implementation, we provide the following policies:

* [Voronoi Diagram Policy](#voronoi_diagram_policy)
* [Delaunay Triangulation Policy](#delaunay_triangulation_policy)
* [Convex Hull Policy](#convex_hull_policy)

### Voronoi Diagram Policy

This policy is implemented by the function *voronoidiagrampolicy* (with dependency of the R packages [deldir](https://cran.r-project.org/web/packages/deldir/deldir.pdf), [sp](https://cran.r-project.org/web/packages/sp/sp.pdf), and [rgeos](https://cran.rstudio.com/web/packages/rgeos/rgeos.pdf)), which has the following required parameters:

* **lp**: It is the data frame returned by a fuzzification policy of the fuzzification stage. Therefore, the structure of this data frame should not be modified (but you can modifiy, for example, the name of the columns).
* **c**: It consists of a list of classes that identicates the meaning of each column, after the columns *x* and *y*, of the **lp**. For instance, it corresponds to **classes** if you use the fuzzy set policy, and it corresponds to the name of the generated *k* groups of the fuzzy clustering policy.
* **basepoly**: It specifies the polygon in which the points are contained. It is employed to establish the boundary limits of the voronoi cells.
* **refin**: It specifies if the voronoi cells should be inside the **basepoly** only (*false*). Otherwise (*true* and its default value), the voronoi cell intersecting the **basepoly** are refined by using the intersection operation between the voronoi cell and the **basepoly**; it may require more processing time.

This policy returns a matrix containing the following columns: 

* *c* is the same classes specified by **c**.
* another column that represents the plateau region object representing a specific class.

### Delaunay Triangulation Policy

This policy is implemented by the function *delaunaytriangulationpolicy* (with dependency of the R packages [deldir](https://cran.r-project.org/web/packages/deldir/deldir.pdf), [sp](https://cran.r-project.org/web/packages/sp/sp.pdf), which has the following required parameters:

* **lp**: It is the data frame returned by a fuzzification policy of the fuzzification stage. Therefore, the structure of this data frame should not be modified (but you can modifiy, for example, the name of the columns).
* **c**: It consists of a list of classes that identicates the meaning of each column, after the columns *x* and *y*, of the **lp**. For instance, it corresponds to **classes** if you use the fuzzy set policy, and it corresponds to the name of the generated *k* groups of the fuzzy clustering policy.
* **basepoly**: It specifies the polygon in which the points are contained. It is employed to establish the boundary limits of the triangles.
* **refin**: It specifies if the triangles should be inside the **basepoly** only (*false*). Otherwise (*true* and its default value), the triangles intersecting the **basepoly** are refined by using the intersection operation between the voronoi cell and the **basepoly**; it may require more processing time.

This policy returns a matrix containing the following columns: 

* *c* is the same classes specified by **c**.
* another column that represents the plateau region object representing a specific class.

### Convex Hull Policy

*To be specified.* 

## Running Example

We have employed this implementation to extract plateau region objects from a real-world data set representing the average temperature for the year 1970-2000. This data set can be downloaded at [World Clim Version 2](http://worldclim.org/version2). We are preparing the step-by-step of this running example.