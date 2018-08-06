---
title: "FISH-ProDe Installation"
---

# How to install FISH-ProDe

* Clone the git repository locally.

```bash
git clone https://github.com/ggirelli/ood-fish/
cd ood-fish
```

* Install Python2 dependencies (requires pip2, installed with `sudo apt install python-pip` or similar).

```bash
sudo -H pip2 install sqlite3 matplotlib numpy pandas scipy shutil urllib2 xml zipfile
```

* Install Python3 dependencies (requires pip3 and python3, installed with `sudo apt install python3 python3-pip` or similar).

```bash
sudo -H pip3 install bottle numpy pandas paste
```

* Download/Extract databases. More details on the [database page](https://ggirelli.github.io/fish-prode/database).