---
title: "FISH-ProDe Usage"
---

# How to run FISH-ProDe

## Web interface

For more details, check the [web interface page](https://ggirelli.github.io/fish-prode/web_interface).

## Command line

`FISH-ProDe` can also be run from command line by running the `design_probes.py` script, which allows to **identify the best FISH probe** in a specific genomic region. Specifically, it provides a number of candidates from which the user can choose its favorite. If we run `design_probes.py -h` we get a useful recap of all the options:

```
usage: design_probes.py [-h] [--description descr] [--feat_order fo]
                         [--f1_thr ft] [--min_d md] [--n_oligo no]
                         [--n_probes np] [--max_probes mp] [--win_shift ws]
                         [--outdir od] [-f [F]]
                         id name chr start end db

Query database for a FISH probe.

positional arguments:
  id                   Query ID.
  name                 Query name.
  chr                  Chromosome in "ChrXX" format.
  start                Probe range starting position.
  end                  Probe range ending position.
  db                   Database folder path.

optional arguments:
  -h, --help           show this help message and exit
  --description descr  Query description
  --feat_order fo      Comma-separated features.
  --f1_thr ft          Threshold of first feature filter, used to identify a
                       range around the best value. It's the percentage range
                       around it. Accepts values from 0 to 1.
  --min_d md           Minimum distance between consecutive oligos.
  --n_oligo no         Number of oligos per probe.
  --n_probes np        Number of probes to design.
  --max_probes mp      Maximum number of output probe candidates. Set to "-1"
                       to retrieve all candidates.
  --win_shift ws       Window size fraction for shifting the windows.
  --outdir od          Query output directory.
  -f [F]               Force overwriting of the query if already run.

```

Probe characteristics
---------------------

The script focuses on three possible probe characteristics:

* **Size** (![I_i]). The size of the genomic regione covered by the probe. It is calculated as the difference between the end position of the last ![k]-mer (![E]) and the start position of the first ![k]-mer (![S]).

![Iiform]

* **Centrality** (![C_i]). It measures how centrally the probe is located in the specified Genomic Region of Interest (GRoI). Specifically, it takes values between 0 and 1, where 1 means perfectly central and 0 means perfectly borderline. Mathematically speaking, if [!S_g] and [!E_g] are respectively the start and end position of the GRoi, then

![MMCform]

With ![M_g] and ![M_i] being the middle points of the GRoI and of the ![i]-th probe, respectively, and ![dab] being the distance between the points `A` and `B`.

* **Spread** (![P_i]). It measures how homogeneously the oligomers are spread over the probe. It is basically the inverse of the consecutive-mers distance's standard deviation. Thus, the larger ![P_i], the more homogeneously the oligomers are spread.

![UPform]

It is important to note how size and spread need to be minimized, while centrality should be maximized.

Algorithm
---------

The algorithm behind the single probe design considers a probe candidate as a set of ![N_O] consecutive oligomers (or ![k]-mers), in the genomic region of interest. Two ![k]-mers are considered **consecutive** when there are no other ![k]-mers between them.

It starts by checking that the number of requested ![k]-mers can actually fit the specified GRoI. Otherwise, it throws an error. Keeping in mind that the ``uniqueOligo`` pipeline forces a minimum distance ![min_d] between consecutive ![k]-mers, the minimum size of a GRoI is

![minIG]

If the query passes the first test, the tool proceeds with the generation of all probe candidates ![C]. This is achieved by ![N_O] grouping consecutive ![k]-mers in ![C].

![Ciform]

Where ![O_i] is the ![i]-th ![k]-mers in the GRoI and ![C_i] is the ![i]-th probe candidate. If the GRoI has ![N_G] ![k]-mers, then [Nform] probe candidates are generated.

The algorithms requires to rank the probe characteristics (size, centrality, and spread) in so-called 1st, 2nd and 3rd *features* (![f_1], ![f_2], and ![f_3]).

![best1]
![best2]

Then, the 1st feature is calculated for every probe candidate ![C] and the best probe candidate is identified. An interval around the best candidate 1st feature value is calculated using the user-provided threshold ![t].

![Iform]

Every candidate probe ![C_i] with an [fnot] is discarded.

Then, ![f_2] and ![f_3] are calculated for every remaining probe candidate. The candidates are ranked based on ![f_2] \(with the `best` on top) and returned as the output.

The tool also produces plots to easily understand how the probe is structured.

[k]: http://chart.apis.google.com/chart?cht=tx&chl=k
[i]: http://chart.apis.google.com/chart?cht=tx&chl=i
[t]: http://chart.apis.google.com/chart?cht=tx&chl=t
[S]: http://chart.apis.google.com/chart?cht=tx&chl=S
[E]: http://chart.apis.google.com/chart?cht=tx&chl=E
[C]: http://chart.apis.google.com/chart?cht=tx&chl=C
[I_i]: http://chart.apis.google.com/chart?cht=tx&chl=I_i
[C_i]: http://chart.apis.google.com/chart?cht=tx&chl=C_i
[M_g]: http://chart.apis.google.com/chart?cht=tx&chl=M_g
[M_i]: http://chart.apis.google.com/chart?cht=tx&chl=M_i
[P_i]: http://chart.apis.google.com/chart?cht=tx&chl=P_i
[S_g]: http://chart.apis.google.com/chart?cht=tx&chl=S_g
[E_g]: http://chart.apis.google.com/chart?cht=tx&chl=E_g
[N_O]: http://chart.apis.google.com/chart?cht=tx&chl=N_O
[f_1]: http://chart.apis.google.com/chart?cht=tx&chl=f_1
[f_2]: http://chart.apis.google.com/chart?cht=tx&chl=f_2
[f_3]: http://chart.apis.google.com/chart?cht=tx&chl=f_3
[dab]: http://chart.apis.google.com/chart?cht=tx&chl=d(A,B)
[min_d]: http://chart.apis.google.com/chart?cht=tx&chl=min_d
[O_i]: http://chart.apis.google.com/chart?cht=tx&chl=O_i
[N_G]: http://chart.apis.google.com/chart?cht=tx&chl=N_G
[fnot]: http://chart.apis.google.com/chart?cht=tx&chl=f_{1,i}\notin{I_{f_1}}
[minIG]: http://mathurl.com/y9kfy2az.png
[Ciform]: http://mathurl.com/yc9to77j.png
[best1]: http://mathurl.com/y8jsn7k2.png
[best2]: http://mathurl.com/y8sh9pos.png
[Iform]: http://mathurl.com/yaebla63.png
[Nform]: http://mathurl.com/y9aorugn.png
[Iiform]: http://chart.apis.google.com/chart?cht=tx&chl=I_i=E_i-S_i
[MMCform]: http://mathurl.com/yaq6xfzw.png
[UPform]: http://mathurl.com/y74watg9.png
