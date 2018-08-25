**FISH Pro**be **De**sign (**FISH-ProDe**, pronounced *pro‧de*, "brave" or "valiant" in italian) is a suite of tools for selection of complementary oligonucleotides to build FISH probes. It also includes a web interface to simplify the selection and remove any need for programming skills.

The suite allows to select sets of oligomers as FISH probes from databases of **non-overlapping** complementary oligonucleotides. Every database is expected to be a folder with one txt file per chromosome, containing the starting location of each oligo. The length of the oligos is encoded in the folder name.

The `fprode_dbextract` command can be used to convert a `sqlite3` database into single-chromosome txt files in the aforementioned format. `fprode_dbquery` allows instead to extract probes from a database based on a number of parameters that can be easily tweaked by the user. For simplicity, a web-interface is available with `fprode_serve`. More details in the [usage page](https://ggirelli.github.io/fish-prode/usage).

While the current implementation does not allow for overlapping oligonucleotides in the database, we are planning to take that into account.

## Useful links

* [Install](https://ggirelli.github.io/fish-prode/install)
* [Usage](https://ggirelli.github.io/fish-prode/usage)
    - [Database](https://ggirelli.github.io/fish-prode/database)
    - [Web Interface](https://ggirelli.github.io/fish-prode/web_interface)
* [Contributing Guidelines](https://ggirelli.github.io/fish-prode/contributing)
* [Code of Conduct](https://ggirelli.github.io/fish-prode/code_of_conduct)