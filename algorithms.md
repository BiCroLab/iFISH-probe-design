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

The single probe design algorithms requires the following inputs:

* A database of FISH oligonucleotides.
* The genomic region of interest, *e.g.*, `chr1:1000000-1001000`.
* The number of oligos for the probe (*N<sub>O</sub>*).
* The priority order for the aforementioned features. Default is: (1) `size`, (2) `homogeneity`, and (3) `centrality`.
* A range (fraction, *F*) for the filter step, which is 0.1 by default.

The algorithm performs the following steps:

1. Retrieve all oligonucleotides in the region of interest, from the database.
2. Identify all sets of *N<sub>O</sub>* consecutive oligonucleotides from the retrieved ones.
3. Calculate the three features for each oligonucleotide set.
4. Discard all sets that have a priority 1 feature (`size` by default) outside a range around the *best value*. This step behaves differently depending on the feature, using the following ranges:
    * `size`: `min(size)±F*min(size)`
    * `homogeneity`: `max(homogeneity)±F*max(homogeneity)`
    * `centrality`: `max(centrality)±F*max(centrality)`
5. Sort the remaining sets based on the priority 2 feature (`homogeneity` by default), from the *best* to the *worst* value. This step behaves differently depending on the feature, sorting as follows:
    * `size`: from `min(size)` to `max(size)`
    * `homogeneity`: from `max(homogeneity)` to `min(homogeneity)`
    * `centrality`: from `max(centrality)` to `min(centrality)`
6. Provide as output the first set in the sorted list, which is considered to be the *optimal* probe.

##  Spotting probe design

### Features

* `homogeneity` of inter-probe distance and probe size: defined as the average between the reciprocal of the standard deviation of inter-probe distance and probe size, respectively. The distance between two consecutive probes is the difference in genomic coordinates between the last base covered by the last oligo in the first probe, and the first base covered by the first oligo in the second probe.

### Algorithm

The spotting probe design algorithms requires the following inputs:

* A database of FISH oligonucleotides.
* The genomic region of interest, *e.g.*, `chr1:1000000-1001000`.
* The number of probes to be designed (*N<sub>P</sub>*)
* The number of oligos for a probe (*N<sub>O</sub>*).
* The priority order for the aforementioned features. Default is: (1) `size`, (2) `homogeneity`, and (3) `centrality`.
* A range (fraction, *F*) for the filter step, which is 0.1 by default.

The algorithm works as following:

1. Retrieve all oligonucleotides in the region of interest, from the database.
2. Identify all sets of *N<sub>O</sub>* consecutive oligonucleotides from the retrieved ones.
3. Calculate the three features for each oligonucleotide set.
4. ...