---
title: Database
---

`ifpd` uses databases of oligonucleotide sequences designed for fluorescence *in situ* hybridization (FISH). In other words, these sequences are designed to hybridize to a single genomic locus with high specificity at certain FISH conditions.

In `ifpd`, each database consist of a folder with one file per chromosome, and a `.config` file. In other words, the structure of a database looks something like this:

```
database_folder
    ┣ chr1
    ┣ chr2
    ┣ ...
    ┣ chrN
    ┗ .config
```

To see how to generate a database, check the description of the [`ifpd_mkdb`]({{ site.baseurl }}/scripts#ifpd_mkdb) script.

### The chromosome files

Each chromosome file is a plain text file containing at least two columns: `start` position, `end` position. A third `sequence` column, containing the sequence corresponding to the `start-end` region can be stored in the database. Start and end position are expected to respect follow the [UCSC BED file format](https://genome.ucsc.edu/FAQ/FAQformat.html#format1), *i.e.*:

* **start**: yhe starting position of the feature in the chromosome. The first base in a chromosome is numbered 0. The `start` position in each BED feature is therefore interpreted to be 1 greater than the `start` position listed in the feature. For example, `start=9`, `end=20` is interpreted to span bases 10 through 20, inclusive.
* **end**: the ending position of the feature in the chromosome . The end position in each BED feature is one-based. Hence, the `end` base is not included in the display of the feature. For example, the first 100 bases of a chromosome are defined as `start=0`, `end=100`, and span the bases numbered 0-99.

In very specific applications or setups, it might be necessary to use databases without the `sequence` column, to minimize the required storage space. In such cases, `ifpd` will retrieve the sequences from the UCSC server. Since this process is relatively slow and time-consuming, it is anyhow advised against.

Moreover, at the moment of generation, it is possible to retain in the database any number of additional columns. These are anyhow not used by the `ifpd` package.

### The `.config` file

The `.config` file is automatically generated alongside the databases. It is used for compatibility with the whole `ifpd` package, and to validate a newly generated databases. This file tracks a number of features and parameters of the database, alongside custom ones that the user can add when generating it. An example of `.config` file is the following:

```
[DATABASE]
name = databaseName
refgenome = hg19

[OLIGOS]
sequence = True
min_dist = 10
min_length = 40
max_length = 40
overlaps = False

[SOURCE]
bed = /media/test/MYC.bed
enforced2bed3 = False
outdirectory = /media/test/MYC

[CUSTOM]
url = example.com
```

Here is the meaning of each field:

* `DATABASE`
    - `name`: name of the database, used by the web interface.
    - `refgenome`: reference genome, for compatibility purposes.
* `OLIGOS`
    - `sequence`: whether the database contains the sequence column.
    - `min_dist`: minimum distance between consecutive oligos (`end` of the first, `start` of the second).
    - `min_length`, `max_length`: oligos length range.
    - `overlaps`: whether the database contains overlapping oligos.
* `SOURCE`
    - `bed`: the input BED-like file used to generate the database with `ifpd_mkdb`.
    - `enforced2bed3`: whether the input BED-like file was forced to BED3 format.
    - `outdirectory`: database directory.
* `CUSTOM`
    - Any custom field added by the user will/should be stored here.
