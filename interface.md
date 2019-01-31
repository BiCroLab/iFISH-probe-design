---
title: ifpd web interface
---

A brief description on how to run the interface with `ifpd_serve` is available in [the corresponding page]({{ site.baseurl }}/scripts#ifpd_serve) page. 

Additionally, some examples are also available [here]({{ site.baseurl }}/examples).

The interface is fully responsive, and can be visualized with a display of any size or aspect ratio. Still, we suggest using a large enough display to properly visualize details in some plots without having to download them or zomm in.

#### Content

* [Homepage](#homepage)
    - [Single probe](#single-probe)
    - [Spotting probe](#spotting-probe)
    - [Queue](#queue)
    - [Search](#search)
* [Query page](#query-page)
* [Probe candidate page](#probe-candidate-page)
* [Probe set candidate page](#probe-set-candidate-page)

## Homepage

![homepage]({{ site.baseurl }}/images/homepage.png)

The homepage starts with a big header banner with the text **iFISH probe designer**, immediately followed by a small disclaimer text and then by the main interface body (<span style="color: red;">red</span> bounding box in the screenshot).

<p class="mb-1">The main interface body is divided in 5 main tabs, plus two additional buttons:</p>

* **Single probe** contains the form to design a single probe.
* **Spotting probe** contains the form to design a spotting probe.
* **Databases** shows details regarding the currently available databases.
* **Queue** shows the queue status and whether there are queries waiting to be executed.
* **Search (<span class="fas fa-search"></span>)** allows to input a query ID to return to the corresponding query page. An "Error 500" message is shown if the specified query ID does not exist.
* **Help (<span class="fas fa-info-circle"></span>)** redirects to this page.
* **Genome Browser (<span class="fas fa-dna"></span>)** redirects to the [UCSC genome browser](http://genome.ucsc.edu/cgi-bin/hgTracks). This can be useful to obtain the coordinates of genes or other genomic regions of interest.

More details on each tab in the corresponding sub-sections below.

The footer of the page reports the version tag and copyright details. When visiting this documentation, always check that the version tags match!

### Single probe

The single probe design form is divided into four main areas (or "cards").

![form-general-card]({{ site.baseurl }}/images/form-general-card.png)

The **General** card (light-blue background) asks for a *name* and a *description* for the query. These are both optional and provided for your convenience to remember the details (*e.g.*, purpose, experiment,...) of your query.

![form-where-card]({{ site.baseurl }}/images/form-where-card.png)

In the **Where** card, you can select the database from which to retrieve the oligos and your genomic region of interest.

![form-single-what-card]({{ site.baseurl }}/images/form-single-what-card.png)

In the **What** card you provide the number of oligonucleotides you want to have in your probe, the fraction (*F*) that the [algorithm]({{ site.baseurl }}/algorithms) should use for the filter step, and how many probes you want in output (set to `-1` to obtain all possible candidates).

![form-advanced-card]({{ site.baseurl }}/images/form-advanced-card.png)

In the **Advanced settings** card you can specify the priority of the three single probe features. For more details on how this is used, check the [algorithm]({{ site.baseurl }}/algorithms) or the [example]({{ site.baseurl }}/examples) pages.

Finally, the big <span class="text-success">green</span> "submit" button sends the form information to the server, that places the query in the queue and redirects you to your query page.

### Spotting probe

The spotting probe design form is identical to the [single probe](#single-probe), with only one difference.

![form-spotting-what-card]({{ site.baseurl }}/images/form-spotting-what-card.png)

In the **What** card, the *Max output probes* field is replaced by the two fields, where you can specify the number of iFISH probes you need for the spotting probe, and the window shift (*W*). For more details on how this is used, check the [algorithm]({{ site.baseurl }}/algorithms) or the [example]({{ site.baseurl }}/examples) pages.

## Query page

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minima laudantium voluptates et saepe odio earum expedita non consectetur aliquid, molestias. Eaque explicabo assumenda quaerat fugiat magni earum delectus excepturi molestiae!

## Probe candidate page

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Labore sed, culpa adipisci corporis saepe corrupti a quis doloremque ratione commodi velit veritatis dolores, minus blanditiis quasi veniam. Odit totam, est.

## Probe set candidate page

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.