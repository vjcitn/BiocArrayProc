## Welcome to BiocArrayProc

### Overview

The purpose of this gh-pages site is to collect links and
comments concerning array processing methods relevant to
Bioconductor.  

#### Software design concepts

A common objective is to hide complexities of working with very
large data while permitting great flexibility in use of
available computing resources.  There are many tradeoffs to
be navigated, and a comprehensive account of the issues will take
substantial work.  A brief sketch follows.

- _**Runtime control of RAM usage.**_  Canonical examples of working
with R typically assume all data are available for immediate
random access: the iris dataset, mtcars.  In the Bioconductor
context, examples include golubEsets, ALL.  From the perspective
of array processing for genomics, we want interactive or batch computations that
    - address arbitrary subarrays of any array of interest
    - limit RAM consumption to subarray scale

    "On-disk" management of array data can take various forms and
    is handled in various packages.
    - ff
    - bigmemory
    - RSQLite, bigrquery for RDBMS-oriented approaches
    - rhdf5
    - matter

    Sparse matrix representations are also relevant.

    The new ALTREP concepts of base R are also relevant.

- _**Configurable parallelism for array operations.**_  This topic is substantial
and can be tackled at various levels.  The most basic concerns
seem to be:
    - Stay out of the way of implicit parallelism achievable for primitive
operations, e.g., as discussed by Roger Peng (https://simplystatistics.org/2016/01/21/parallel-blas-in-r/).
    - Foster parallelized distributed computation on subarrays 
whenever relevant.


- _**Lazy computation.**_  The idea here is that we defer
computations as long as possible, to take advantage of reductions
in computational effort that may arise from filtering

- _**Informed assessment of new technologies.**_  This is a complex
topic and aspects that are specifically relevant to genomic
workflows should be identified.  Apache Spark is of 
definite interest, and many approaches
to analysis-oriented storage deserve attention.  
The [Ursa Labs](https://ursalabs.org/tech/) roadmap page has many relevant references.

#### Exemplary documents, packages, datasets, and repositories

##### Documents

- Aaron Lun's [simpleSingleCell workflow](https://bioconductor.org/packages/release/workflows/vignettes/simpleSingleCell/inst/doc/bigdata.html) addresses aspects of storage and approximate
matrix decompositions.

- The [Orchestrating Single Cell Analysis (OSCA)](https://github.com/Bioconductor/OSCABase/) project includes
an Rmarkdown file with an overview of [big-data methods](https://github.com/Bioconductor/OSCABase/blob/master/analysis/big-data.Rmd).

- Peter Hickey's [Bioc 2019 workshop](https://github.com/PeteHaitch/BioC2019_DelayedArray_workshop/blob/master/vignettes/Effectively_using_the_DelayedArray_framework_for_users.Rmd) on DelayedArray provides many details.

##### Packages

- [TENxBrainData](https://github.com/Bioconductor/TENxBrainData).  This
package includes a vignette that helps us understand the roles of
DelayedMatrix and HDF5:

```
> assay(tenx)
<27998 x 1306127> DelayedMatrix object of type "integer":
           AAACCTGAGATAGGAG-1 ... TTTGTCATCTGAAAGA-133
    [1,]                    0   .                    0
    [2,]                    0   .                    0
    [3,]                    0   .                    0
    [4,]                    0   .                    0
    [5,]                    0   .                    0
     ...                    .   .                    .
[27994,]                    0   .                    0
[27995,]                    1   .                    0
[27996,]                    0   .                    0
[27997,]                    0   .                    0
[27998,]                    0   .                    0
```

Additionally, the vignette presents issues involved with 
a sparse representation, managed in this case in HDF5:

```
> h5ls(fname)
  group       name       otype  dclass        dim
0     /       mm10   H5I_GROUP                   
1 /mm10   barcodes H5I_DATASET  STRING    1306127
2 /mm10       data H5I_DATASET INTEGER 2624828308
3 /mm10 gene_names H5I_DATASET  STRING      27998
4 /mm10      genes H5I_DATASET  STRING      27998
5 /mm10    indices H5I_DATASET INTEGER 2624828308
6 /mm10     indptr H5I_DATASET INTEGER    1306128
7 /mm10      shape H5I_DATASET INTEGER          2
```

- [restfulSE](https://f1000research.com/articles/8-21) deals with access
to remote array data in HDF Scalable Data Service or Google BigQuery.

##### Repositories

- recount2
- conquer
- ExperimentHub


#### Key data structures

- SummarizedExperiment
- GenomicRanges
- SingleCellExperiment
- TreeSummarizedExperiment


### Support or Contact

Have a look at the scalability channel at community-bioc.slack.com
