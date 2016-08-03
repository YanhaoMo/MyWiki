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

then, execute `gpg --gen-key` command and follow the instruction to generate a key. You can refer to here[^2] for more information about openGPG.

# Configure reprepro
Once you have your OpenPGP key ready. You can start configuring reprepro.

First, create the reprepro configration directory.

```bash
sudo mkdir -p /var/www/repos/apt/debian/conf
```

then, create the configuratin file. the name of the configration file is "distrbution", put it into `conf` directory.

```bash
cat /var/www/repos/apt/debian/conf
Origin: Your project name
Label: Your project name
Codename: <osrelease>
Architectures: i386 amd64
Components: main
Description: Apt repository for project x
SignWith: <key-id>
```

third, add the second configuration file named "option" at the same position.

```bash
cat /var/www/repos/apt/debian/option
verbose
basedir /var/www/repos/apt/debian
ask-passphrase
```

# (Optional) useing package form other mirror
this can be down by reprepro using `overrides`.

For example, if you want to use package for debian's official repository.

# Links
[^1]: [https://mirrorer.alioth.debian.org/](https://mirrorer.alioth.debian.org/)
[^2]: []()