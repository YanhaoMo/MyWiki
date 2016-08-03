# Overview
This article discribe how to create a Debian package mirror with reprepro[^1] step by step.

# install reprepro package
First of all, Let's install `reprepro` using package manager.

Assume that you are using Debian or Debain-based distribution. Just run the followint command:

```bash
sudo apt update && apt install reprepro
```
# Create OpenPGP key
OpenPGP key is used to sign the package matedata and the *.changes *.dsc file，
It's nessessry for create a debaian package mirror.

`gunpg` is the right thing can help us to do this。
It should be installed in your system by default. If not, install it manually.

```bash
sudo apt install gunpg
```

# Links
[^1]: [https://mirrorer.alioth.debian.org/](https://mirrorer.alioth.debian.org/)