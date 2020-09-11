![fruits of provenance](fruits-of-provenance.png)

## Provenance Tools for R

Our tools for the R statistical language are part of a larger project on [End-to-end-provenance](https://github.com/End-to-end-provenance/End-to-end-provenance.github.io/blob/master/README.md). Please see below for a brief description  of these tools. Additional information may be found in the README files on the various repositories. For details on individual functions, please see the man pages for each package. Note that exported functions generally begin with "prov." to avoid confusion with variable or function names in your scripts or in other libraries.

* [*rdtLite*](https://github.com/End-to-end-provenance/rdtLite/blob/master/README.md) is a light-weight provenance collection tool that collects provenance as an R script executes (or during a console session) and saves it in extended PROV-JSON format to the file prov.json.  By default, this file is written to the R session temporary directory (to meet CRAN requirements) and is overwritten in subsequent executions of the same script (or console session), but you can choose to save it elsewhere and to save time-stamped versions if desired.  Simple data values are automatically saved in the prov.json file.  Complex data values (e.g. R lists or data frames) may optionally be saved (wholly or in part) as separate snapshot files.

* [*rdt*](https://github.com/End-to-end-provenance/rdt/blob/master/README.md) is the research version of our provenance collection tool.  It includes all of the functions and functionality of rdtLite and, in addition, collects provenance inside user functions and control constructs.  It does this by creating and executing an annotated version of the original R script.  While this works in most cases, we’ve found that it can lead to problems in cases of deeply nested functions and control constructs, so we are working on a different solution that will use the R trace function to collect provenance inside functions.

* [*provSummarizeR*](https://github.com/End-to-end-provenance/provSummarizeR/blob/master/README.md) creates a concise high-level summary of the provenance collected by rdtLite or rdt, including information about computing environment, loaded libraries, sourced scripts, and inputs & outputs.

* [*provViz*](https://github.com/End-to-end-provenance/provViz/blob/master/README.md) provides an R interface to a visualization tool, written in Java, that allows you to view and query the provenance graph directly.  You will need to have Java installed for this to work.

* [*provDebugR*](https://github.com/End-to-end-provenance/provDebugR/blob/master/README.md) uses the provenance collected by rdtLite or rdt to support time-traveling debugging of an R script without the need to set breakpoints or insert print statements and rerun the script.

* [*provExplainR*](https://github.com/End-to-end-provenance/provExplainR/blob/master/README.md) uses the provenance collected by rdtLite or rdt from two different executions of a script to help explain why the script results differ.

* [*provTraceR*](https://github.com/End-to-end-provenance/provTraceR/blob/master/README.md) uses the provenance collected by rdtLite or rdt for a single R script or a series of R scripts to identify input files, output files, and exchanged files based on file hash values.

* [*provAnalyzeR*](https://github.com/End-to-end-provenance/provAnalyzeR/blob/master/README.md) uses the provenance collected by rdtLite or rdt to identify and report coding anomalies (under development).

* [*provClean*](https://github.com/End-to-end-provenance/provClean/blob/master/README.md) uses the provenance collected by rdtLite or rdt to create a simplified version of the original R script that contains only those statements needed to produce a specified result (under development).

## Installation

Our tools are implemented as R packages. To get the most recent versions, we recommend installing them from GitHub using the install_github function in the devtools package:

* *rdtLite:* `devtools::install_github("End-to-end-provenance/rdtLite")`
* *rdt:* `devtools::install_github("End-to-end-provenance/rdt")`
* *provSummarizeR:* `devtools::install_github("End-to-end-provenance/provSummarizeR")`
* *provViz:* `devtools::install_github("End-to-end-provenance/provViz")`
* *provDebugR:* `devtools::install_github("End-to-end-provenance/provDebugR")`
* *provExplainR:* `devtools::install_github("End-to-end-provenance/provExplainR")`
* *provTraceR:* `devtools::install_github("End-to-end-provenance/provTraceR")`
* *provAnalyzeR:* `devtools::install_github("End-to-end-provenance/provAnalyzeR")`
* *provClean:* `devtools::install_github("End-to-end-provenance/provClean")`

Note: provSummarizeR, provExplainR, provTraceR, and provAnalyzeR require the provParseR package. provClean and provDebugR require both provParseR and provGraphR. If these do not install automatically they may be installed as follows:

* *provParseR:* `devtools::install_github("End-to-end-provenance/provParseR")`
* *provGraphR:* `devtools::install_github("End-to-end-provenance/provGraphR")`

*rdtLite*, *provSummarizeR*, *provViz*, *provTraceR*, *provParseR*, and *provGraphR* are also available on [*CRAN*](https://cran.r-project.org/).

## Getting Started

We recommend starting with the *rdtLite* package, which collects enough provenance for most purposes. For details on how to load and use *rdtLite*, please see the README file for the *rdtLite* repository. Applications such as *provSummarizeR* and *provViz* can use provenance stored in memory from the most recent script execution or console session with *rdtLite*, or use provenance from an earlier script execution or console session stored in a prov.json file.

## Notes for Developers

* The source code for *rdt* and *rdtLite* is contained in the *RDataTracker* [repository](https://github.com/End-to-end-provenance/RDataTracker). A script is run nightly to create separate repos for each tool to facilitate GitHub installations.  If you’d like to see the long history of code development and issues for *rdt* and *rdtLite*, or enter new issues, please see the *RDataTracker* repository.

* The *RDataTracker* repository contains the necessary files to build and install *rdt* and *rdtLite* and to run extensive regression tests using Apache Ant. To do this, clone the *RDataTracker* repo and see the file README_Build_and_Test.md.

* The [*provParseR*](https://github.com/End-to-end-provenance/provParseR/blob/master/README.md) package facilitates access to the provenance information collected by rdt and rdtLite. The prov.parse function accepts this information as a string or file in extended PROV-JSON format and returns it as an R object. Access functions then extract the desired information from this object and returns it as a data frame. This package supports other packages and is not intended to be used directly.

* The [*provGraphR*](https://github.com/End-to-end-provenance/provGraphR/blob/master/README.md) package creates an adjacency matrix from the provenance object created by provParseR.  The adjacency matrix can then be used to quickly traverse the provenance graph. This package supports other packages and is not intended to be used directly.

* We welcome comments on the [extended PROV-JSON](https://github.com/End-to-end-provenance/ExtendedProvJson/blob/master/JSON-format.md) format used by our provenance collection tools and applications

Tree silhouette from: http://www.vinylsilhouettes.com

