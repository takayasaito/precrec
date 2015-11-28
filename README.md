precrec
=======

The aim of `precrec` is to provide various tools that enable robust performance evaluations of binary classifiers. Specifically, `precrec` offers accurate calculations of ROC and Precision-Recall curves.

All the main calculations of `precrec` are implemented with C++/[Rcpp](https://cran.r-project.org/web/packages/Rcpp). The package structure and the coding style of `precrec` are based on two Hadley Wickham's books - [Advanced R](http://adv-r.had.co.nz/) and [R packages](http://r-pkgs.had.co.nz/).

See our website - [Classifier evaluation with imbalanced datasets](https://classeval.wordpress.com/) - for useful tips for performance evaluation on binary classifiers. In addition, we have summarized potential pitfalls of ROC plots with imbalanced datasets. See our paper - [The Precision-Recall Plot Is More Informative than the ROC Plot When Evaluating Binary Classifiers on Imbalanced Datasets](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0118432) - for more details.

Installation
------------

-   ~~Install the release version of `precrec` from CRAN with `install.packages("precrec")`~~ (Not available at CRAN yet).

-   Alternatively, you can install a development version of `precrec` from [our GitHub repository](https://github.com/takayasaito/precrec). To install it:

    1.  Make sure you have a working development environment.
        -   **Windows**: Install [Rtools](http://cran.r-project.org/bin/windows/Rtools/).
        -   **Mac**: Install Xcode from the Mac App Store.
        -   **Linux**: Install a compiler and various development libraries (details vary across different flavors of Linux).

    2.  Install `devtools` from CRAN with `install.packages("devtools")`.

    3.  Install `precrec` from the GitHub repository with `devtools::install_github("/takayasaito/precrec")`

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

Moreover, the `precrec` package provides five S3 generics for the S3 object created by the `evalmod` function.

| S3 generic | Package  | Description                                                    |
|------------|:---------|:---------------------------------------------------------------|
| print      | base     | Print the calculation results and the summary of the test data |
| plot       | graphics | Plot performance evaluation measures                           |
| autoplot   | ggplot2  | Plot performance evaluation measures with ggplot2              |
| fortify    | ggplot2  | Prepare a data frame for ggplot2                               |
| auc        | precrec  | Make a data frame with AUC scores                              |

Documentation
-------------

A package vignette - Introduction to precrec - contains the descriptions of the functions with several useful examples. View the vignette with `vignette("introduction", package = "precrec")`.

All the five functions and the S3 generics except for `print` have their own help pages with examples.

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

# The grid and gridExtra packages are required to use multiple panels with autoplot
library(grid)
library(gridExtra)

# Show ROC and Precision-Recall plots
autoplot(sscurves)
```

![](README_files/figure-markdown_github/unnamed-chunk-2-1.png)
