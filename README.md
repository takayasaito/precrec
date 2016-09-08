Precrec
=======

[![Travis](https://img.shields.io/travis/takayasaito/precrec.svg?maxAge=2592000)](https://travis-ci.org/takayasaito/precrec) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/takayasaito/precrec?branch=master&svg=true)](https://ci.appveyor.com/project/takayasaito/precrec) [![codecov.io](https://codecov.io/github/takayasaito/precrec/coverage.svg?branch=master)](https://codecov.io/github/takayasaito/precrec?branch=master) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/precrec)](http://cran.r-project.org/package=precrec)

The aim of `precrec` is to provide an integrated platform that enables robust performance evaluations of binary classifiers. Specifically, `precrec` offers accurate calculations of ROC and Precision-Recall curves. All the main calculations of `precrec` are implemented with C++/[Rcpp](https://cran.r-project.org/package=Rcpp).

Four great features of precrec
------------------------------

### 1. Super accurate

`precrec` provides accurate precision-recall curves.

-   Non-linear interpolation
-   Elongation to the y-axis to estimate the first point when necessary
-   Use of score-wise threshold values instead of fixed bins

Because of this accuracy `precrec` calculates correct AUC scores.

### 2. Ultra fast

`precrec` calculates curves in a matter of seconds even for fairly large datasets. It is much faster than most other performance evaluation tools.

### 3. Various evaluation metrics

`precrec` concurrently calculates precision-recall and ROC curves as well as their AUCs by default. It also offers basic evaluation measures.

-   Error rate
-   Accuracy
-   Specificity
-   Sensitivity, true positive rate (TPR), recall
-   Precision, positive predictive value (PPV)
-   Matthews correlation coefficient
-   F-score

### 4. Supporting functions

`precrec` provides several useful functions that lack in many other evaluation tools.

-   Handling multiple models and multiple test sets
-   Handling tied scores and missing entries
-   Calculation of confidence interval bands when multiple test sets are specified
-   Calculation of partial AUCs
-   Pre- and post-process functions for simple data preparation and curve analysis

Installation
------------

-   Install the release version of `precrec` from CRAN with `install.packages("precrec")`.

-   Alternatively, you can install a development version of `precrec` from [our GitHub repository](https://github.com/takayasaito/precrec). To install it:

    1.  Make sure you have a working development environment.
        -   **Windows**: Install [Rtools](http://cran.r-project.org/bin/windows/Rtools/).
        -   **Mac**: Install Xcode from the Mac App Store.
        -   **Linux**: Install a compiler and various development libraries (details vary across different flavors of Linux).

    2.  Install `devtools` from CRAN with `install.packages("devtools")`.

    3.  Install `precrec` from the GitHub repository with `devtools::install_github("takayasaito/precrec")`.

Functions
---------

The `precrec` package provides the following five functions.

| Function             | Description                                                |
|:---------------------|:-----------------------------------------------------------|
| evalmod              | Main function to calculate evaluation measures             |
| mmdata               | Reformat input data for performance evaluation calculation |
| join\_scores         | Join scores of multiple models into a list                 |
| join\_labels         | Join observed labels of multiple test datasets into a list |
| create\_sim\_samples | Create random samples for simulations                      |

Moreover, the `precrec` package provides seven S3 generics for the S3 object created by the `evalmod` function.

| S3 generic    | Package  | Description                                                    |
|:--------------|:---------|:---------------------------------------------------------------|
| print         | base     | Print the calculation results and the summary of the test data |
| as.data.frame | base     | Convert a precrec object to a data frame                       |
| plot          | graphics | Plot performance evaluation measures                           |
| autoplot      | ggplot2  | Plot performance evaluation measures with ggplot2              |
| fortify       | ggplot2  | Prepare a data frame for ggplot2                               |
| auc           | precrec  | Make a data frame with AUC scores                              |
| part          | precrec  | Set partial curves and calculate AUC scores                    |

Documentation
-------------

A package vignette - [Introduction to precrec](https://cran.r-project.org/web/packages/precrec/vignettes/introduction.html) - contains the descriptions of the functions with several useful examples. View the vignette with `vignette("introduction", package = "precrec")`.

All the five functions and the S3 generics except for `print` have their own help pages with examples. CRAN provides a pdf version of all combined help files as a reference manual ([pdf](https://cran.r-project.org/web/packages/precrec/precrec.pdf)).

Examples
--------

Following two examples show the basic usage of `precrec` functions.

### ROC and Precision-Recall calculations

The `evalmod` function calculates ROC and Precision-Recall curves and returns an S3 object.

``` r
library(precrec)

# Load a test dataset
data(P10N10)

# Calculate ROC and Precision-Recall curves
sscurves <- evalmod(scores = P10N10$scores, labels = P10N10$labels)
```

### Visualization of the curves

The `autoplot` function outputs ROC and Precision-Recall curves by using the `ggplot2` package.

``` r
# The ggplot2 package is required 
library(ggplot2)

# Show ROC and Precision-Recall plots
autoplot(sscurves)
```

![](https://rawgit.com/takayasaito/precrec/master/README_files/figure-markdown_github/unnamed-chunk-2-1.png)

External links
--------------

See our website - [Classifier evaluation with imbalanced datasets](https://classeval.wordpress.com/) - for useful tips for performance evaluation on binary classifiers. In addition, we have summarized potential pitfalls of ROC plots with imbalanced datasets. See our paper - [The Precision-Recall Plot Is More Informative than the ROC Plot When Evaluating Binary Classifiers on Imbalanced Datasets](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0118432) - for more details.

The package structure and the coding style of `precrec` are based on two Hadley Wickham's books - [Advanced R](http://adv-r.had.co.nz/) and [R packages](http://r-pkgs.had.co.nz/).
