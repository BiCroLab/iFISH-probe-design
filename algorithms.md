---
title: Algorithms
---

We included two algorithms in `ifpd`: the first to design a single probe in a genomic region of interest (gROI), and the second to design a number of homogeneously spread probes in a gROI (i.e, to design a *spotting* probe).

Both algorithms are based on the calculation of either single or spotting probe-related features. We will go more into the details of both features and algorithms in the following sections.

##  Single probe design

### Features

* `size`: defined as the distance between the genomic coordinates of the first base covered by the first oligo, and the last base covered by the last oligo.
* `centrality`: ratio between the distance between the gROI midpoint and the probe midpoint, and the gROI's half-size. It spans from 0, when the probe midpoint sits on the gROI's border, to 1, when the probe midpoint coincides to the gROI's midpoint.
* `homogeneity` of inter-oligo distance: defined as the reciprocal of the inter-oligo distance standard deviation. The distance between two consecutive oligos is defined as the difference in genomic coordinates of the last base covered by the first oligo, and the first base covered by the second oligo.

### Algorithm

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

##  Spotting probe design

### Features

* `homogeneity` of inter-probe distance and probe size: defined as the average between the reciprocal of the standard deviation of inter-probe distance and probe size, respectively. The distance between two consecutive probes is the difference in genomic coordinates between the last base covered by the last oligo in the first probe, and the first base covered by the first oligo in the second probe.

### Algorithm

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
