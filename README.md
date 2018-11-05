![fruits of provenance](fruits-of-provenance.png)

## Provenance

Provenance is the history of an item of data from its creation to its present state. It includes details about the steps that were executed and the intermediate values that were created in order to produce the data in its current form. For scientists, provenance can help to facilitate reproduction and validation of scientific results.

In this project we are developing tools that collect and use provenance for the R statistical language. Provenance is collected as an R script executes or during an R console session and is stored in an [extended PROV-JSON](prov-json-extension.pdf) format. Applications then use the provenance to perform tasks that support scientists in their work.

## Software Tools

Please see below for a brief description of our tools. Additional information may be found in the README files on the various repositories. For details on individual functions, please see the man pages for each package. Note that exported functions generally begin with "prov." to avoid confusion with variable or function names in your scripts or in other libraries.

* *rdtLite* is a light-weight provenance collection tool that collects provenance as an R script executes (or during a console session) and saves it in extended PROV-JSON format to the file prov.json.  By default, this file is written to the R session temporary directory (to meet CRAN requirements) and is overwritten in subsequent executions of the same script (or console session), but you can choose to save it elsewhere and to save time-stamped versions if desired.  Simple data values are automatically saved in the prov.json file.  Complex data values (e.g. R lists or data frames) may optionally be saved (wholly or in part) as separate snapshot files.

* *rdt* is the research version of our provenance collection tool.  It includes all of the functions and functionality of rdtLite and, in addition, collects provenance inside user functions and control constructs.  It does this by creating and executing an annotated version of the original R script.  While this works in most cases, we’ve found that it can lead to problems in cases of deeply nested functions and control constructs, so we are working on a different solution that will use the R trace function to collect provenance inside functions.

* *provViz* provides an R interface to a visualization tool, written in Java, that allows you to view and query the provenance graph directly.  You will need to have Java installed for this to work.

* *RClean* uses the provenance collected by rdtLite or rdt to create a simplified version of the original R script that contains only those statements needed to produce a specified result.

* *provDebugR* uses the provenance collected by rdtLite or rdt to support time-traveling debugging of an R script without the need to set breakpoints or insert print statements and rerun the script.

## Installation

Our tools are implemented as R packages. We recommend installing them from GitHub using the install_github function in the devtools package:

* *rdtLite:* `install_github("End-to-end-provenance/rdtLite")`
* *rdt:* `install_github("End-to-end-provenance/rdt")`
* *provViz:* `install_github("End-to-end-provenance/provViz")`
* *RClean:* `install_github("ProvTools/RClean")`
* *provDebugR:* `install_github("End-to-end-provenance/provDebugR")`

Note: RClean and provDebugR both require the provParseR and provGraphR packages. If these do not install automatically they may be installed as follows:

* *provParseR:* `install_github("End-to-end-provenance/provParseR")`
* *provGraphR:* `install_github("End-to-end-provenance/provGraphR")`

## Getting Started

We recommend starting with the *rdtLite* package, which collects enough provenance for most purposes. For details on how to load and use *rdtLite*, please see the README file for the *rdtLite* repository. Applications such as *provViz* can use provenance stored in memory from the most recent script execution or console session with *rdtLite*, or use provenance from an earlier script execution or console session stored in a prov.json file.

## Notes for Developers

* The source code for *rdt* and *rdtLite* is contained in the *RDataTracker* repository (https://github.com/End-to-end-provenance/RDataTracker). A script is run nightly to create separate repos for each tool to facilitate GitHub installations.  If you’d like to see the long history of code development and issues for *rdt* and *rdtLite*, or enter new issues, please see the *RDataTracker* repository.

* The *RDataTracker* repository contains the necessary files to build and install *rdt* and *rdtLite* and to run extensive regression tests using Apache Ant. To do this, clone the *RDataTracker* repo and see the file README_Build_and_Test.txt.

* The *provParseR* package facilitates access to the provenance information collected by rdt and rdtLite. The prov.parse function accepts this information as a string or file in extended PROV-JSON format and returns it as an R object. Access functions then extract the desired information from this object and returns it as a data frame. This package supports other packages and is not intended to be used directly.

* The *provGraphR* package creates an adjacency matrix from the provenance object created by provParseR.  The adjacency matrix can then be used to quickly traverse the provenance graph. This package supports other packages and is not intended to be used directly.

* We welcome comments on the [extended PROV-JSON](prov-json-extension.pdf) format used by our provenance collection tools and applications

## Active Contributors

* [Emery Boose](https://harvardforest.fas.harvard.edu/researchers/9), Harvard University

* [Aaron Ellison](https://harvardforest.fas.harvard.edu/aaron-ellison), Harvard University

* [Elizabeth Fong](https://www.linkedin.com/in/elizabethfongwm). Mount Holyoke College

* [Matthew Lau](https://harvardforest.fas.harvard.edu/researchers/8438), Harvard University

* [Barbara Lerner](https://www.mtholyoke.edu/%7Eblerner/), Mount Holyoke College

* [Thomas Pasquier](https://www.cl.cam.ac.uk/%7Etfjmp2/), University of Bristol

* [Margo Seltzer](https://www.eecs.harvard.edu/margo/), University of British Columbia

* [Joseph Wonsil](https://jwons.github.io/), Carthage College

## Past Contributors

* Shay Adams, Mount Holyoke College
* Orenna Brand, Columbia University
* Vasco Carinhas, Universidad de Puerto Rico en Arecibo
* Marios Dardas, Holy Cross College
* Connor Gregorich-Trevor, Grinnell College
* Nikki Hoffler, Mount Holyoke College
* Jen Johnson, Middlebury College
* Andy Kaldunski, Ripon College
* Alex Liu, Amherst College
* Miruna Oprescu, Harvard University
* Luis Perez, Harvard University
* Lia Poulos, Mount Holyoke College
* Moe Pwint Phyu, Mount Holyoke College
* Garrett Rosenblatt, University of Rochester
* Sofiya Taskova, Mount Holyoke College
* Cory Teshera-Sterne, Mount Holyoke Colege
* Morgan Vigil, Westmont College
* Yujia Zhou, Dickinson College

## Acknowledgments

This work was supported by NSF grants DEB-1237491, DBI-1459519, and SSI-1450277, the Charles Bullard Fellowship at Harvard University, and a faculty fellowship from Mount Holyoke College, and is a contribution from the Harvard Forest Long-Term Ecological Research (LTER) program.

Tree silhouette from: http://www.vinylsilhouettes.com
