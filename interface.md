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

The query starts with a big header banner with the text **Query**, immediately followed by a breadcrumb navigation bar, with a dropdown menu on the left and the parents pages.

![query-head]({{ site.baseurl }}/images/query-head.png)

Right after the navigation bar, a gray alert is shown, recommending to either save the link to this page, bookmark it, or note down your query ID. You can use the link to the query page to get back to it, or use the query ID to get back there using the **search** tab in the homepage. You can copy the query ID either by selecting it from the navigation bar (it's that list of characters after "Query: ") or simply by clicking on the "copy your query id" link. To hide this message click on the black cross (<span class="fas fa-times"></span>) on the left.

Then, if the query is not processed immediately but queued instead, a <span class="text-warning">yellow</span> alert reports the queuing time. The page keeps refreshing automatically every 10 seconds while the query is in the queue. If this does not happen, you can do it by clicking on the refresh (<span class="fas fa-redo"></span>) icon on the left.

![query-head-running]({{ site.baseurl }}/images/query-head-running.png)

When the query leaves the queue, the <span class="text-warning">yellow</span> alert changes to report the processing time. At this stage, the page keeps refreshing automatically every 5 seconds. If this does not happen, you can do it by clicking on the refresh (<span class="fas fa-redo"></span>) icon on the left.

![query-head-success]({{ site.baseurl }}/images/query-head-success.png)
![query-head-timeout]({{ site.baseurl }}/images/query-head-timeout.png)

Once the query is processed, the alert turns <span class="text-success">green</span> and reports the time at which the query was completed, alongside the running time. If something wrong happend during the processing, or if the query took too long, the alert turns <span class="text-dange">red</span> and invites the user to try again or contact the server admin.

![query-head-info]({{ site.baseurl }}/images/query-head-info.png)

Right after the query status alert, some info are reported: query name, time of submission, and description. Given that query name and description are optional, sometimes only some of these information are reported.

![query-settings]({{ site.baseurl }}/images/query-settings.png)
![query-cmd]({{ site.baseurl }}/images/query-head-info.png)

In the **Query settings** card, the query parameters are reported. This is similar to the **Cmd** card, where the command line used to run the query is shown.

![query-log]({{ site.baseurl }}/images/query-log.png)

The **Log** card shows the query processing log. This area is updated automatically at each page refresh, and is automatically scrolled to the bottom (most recent update) while the query is being processed.

![query-table]({{ site.baseurl }}/images/query-table.png)
![query-table-figures]({{ site.baseurl }}/images/query-table-figures.png)

When the query has been fully processed, a new card with **Table** and **Figures** tabs appears. These report the query results, respectively in tabular and graphical format. For each candidate reported, a link is available to the candidate page, or to download it as a zip folder.

![query-download]({{ site.baseurl }}/images/query-download.png)

Finally, a big <span class="text-success">green</span> "Download" button allows to download the entirety of the query results in zip format. As per disclaimer, this might take a few moments (up to a few minutes depending on the query size) to generate the zip folder.

## Probe candidate page

![candidate-page]({{ site.baseurl }}/images/candidate-page.png)

The **Probe candidate page** is relatively simple: navigation bar at the top, graphical reports on the candidate in the first card, followed by a **Details** card a three buttons to download the candidate in a variety of formats.

The plots in the first card show the following:

* **Top**: the genomic region spanned by the probe in black, and the location of each oligonucleotide in cyan. Vertical dotted lines indicate the midpoint of each oligonucleotide.
* **Bottom-left**: the genomic region of interest in black and the region spanned by the probe in cyan. The vertical dashed red line indicates the region midpoint, while the vertical cyan dashed line indicates the probe midpoint.
* **Bottom-center**: the ID of each oligo on the x-axis, and its midpoint genomic coordinate on the y-axis. Each oligo is represented by a red dot. First and last oligos are connected by a black line. If all consecutive oligonucleotides were equally spaced, all red dots would fall on the black line.
* **Bottom-right**: density histogram of distance between consecutive oligonucleotides (as defined in the [algorithm]({{ site.baseurl }}/algorithms) page).

## Probe set candidate page

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.