---
title: ifpd scripts
---

You can access the help page of each script by using the `-h` option.

## `ifpd_mkdb`

This script takes a BED-like file of at least three columns (`chromosome`, `start` position, and `end` position), and generates a [database]({{ site.baseurl }}/database) folder in a format compatible with the rest of `ifpd`'s scripts. The input file can contain a fourth optional column with the `sequence` corresponding to each row's region. If that is the case, the sequence can be retained by using the `--retain-sequences`.

The minimum input comprises the BED-like file path, the corresponding reference genome, and a name for the new database. Importantly, the specified reference genome must be in an NCBI-compatible format and available at UCSC. Use the `--list-refGenomes` to show the list of available genomes.

If you want to use a genome available through a DAS server different from the UCSC one, you can specify the DAS server URL with the `--ucsc-das-uri`.

As explained in the [database]({{ site.baseurl }}/database) page, the input BED-like file is expected to respect the UCSC BED format pertaining the indexing of genomic coordinates. If your input file specifies regions with both `start` and `end` positions being inclusive, you can use the `--increment-chrom-end` option to convert it to the appropriate format.

## `ifpd_dbchk`

This script checks a database for proper formatting and compatibility with the `ifpd` package. Some checks require internet connection. Use `--no-net` to skip them. Also, when a connection to the internet is available, use the `--check-seq` to verify that the sequences stored in the database are correct. This sequence-check step is skipped by default due to it being extremely slow.

## `ifpd_query_probe`

This script queries a database to design a single iFISH probe, using the algorithm explained in [the corresponding page]({{ site.baseurl }}/algorithms#single-probe-design).

## `ifpd_query_set`

This script queries a database to design a spotting iFISH probe, using the algorithm explained in [the corresponding page]({{ site.baseurl }}/algorithms#spotting-probe-design).

## `ifpd_serve`

This script can be used to run the `ifpd` [web interface]({{ site.baseurl }}/interface) on your own computer. If run without any parameters, it serves the interface at the `0.0.0.0:8080` address. URL and port can be customized using the `-u` and `-p` options, respectively.