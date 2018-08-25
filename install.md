---
title: "FISH-ProDe Installation"
---

# How to install FISH-ProDe

### From PyPi

Install from pypi with `sudo -H pip3 install fish-prode`, and that's it! That's as easy as it gets.

To **update** run `sudo -H pip3 install -U fish-prode`.

To **remove** run `sudo -H pip3 uninstall fish-prode`, and confirm when prompted.

### From GitHub

You can also **install** from github (any point in history, although we suggest to stick with realease tags) as follows:

```bash
git clone https://github.com/ggirelli/fish-prode/
cd fish-prode
sudo -H pip3 install -e .
```

To **update**, run the following from within the repository folder:

```bash
git pull
sudo -H pip3 install -e .
```
(the second line is needed only to update the package version recognized by pip)

To **uninstall**, run the following from within the repository folder:

```bash
sudo -H python3 setup.py develop --uninstall
```

And then manually remove the scripts files. A list of the installed script files is available in the `setup.py` file. Check their location with `whereis`.