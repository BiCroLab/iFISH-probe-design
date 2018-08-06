---
title: "FISH-ProDe Web Interface"
---

# How to use the FISH-ProDe Web interface

Start the web interface using the `web.py` script. Customized URL and port can be provided with the `--url` and `--port` flags, respectively.

Once the script is running, visit the specified URL (defaults to `0.0.0.0:8080`) and select the **probe design** option.

The available options in the main panel are:

* Index: shows a list of ran/running queries.
* Single probe
    - Query: to submit a single query to design a single probe.
    - Queries: to submit multiple query, to design a single probe each.
* Multi probe: to submit a single query to design a specific number of probes in a region of interest.

The panel on the right (or bottom) allows to see how many and which queries are in the queue. The queries are executed one at a time in a First In First Out (FIFO) way.

More details are available in the help page accessible by pressing the "help" button on the top-right corner of the main panel.