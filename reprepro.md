# Overview
This article discribe how to create a personal Debian package repository with reprepro[^1] step by step.

# install reprepro package
First of all, Let's install `reprepro` using package manager.

Assume that you are running Debian or Debain-based distribution. 
Just execute the following command to get reprepro installed in you system:

```bash
sudo apt update && apt install reprepro -y
```
# Create OpenPGP key
OpenPGP key is used to sign the package matedata and the *.changes *.dsc file，
You must to create you own OpenPGP key to continue.

`gunpg` is the right thing can help us to do this。
It should be installed in your system by default. If not, install it manually.

```bash
sudo apt install gunpg
```

Then, execute `gpg --gen-key` command and follow the instruction to generate a key.
You can refer to here[^2] for more information about openGPG.

# Configure reprepro
Once you have your OpenPGP key ready. You can start configuring reprepro.

First, create the reprepro configration directory.

```bash
sudo mkdir -p /var/www/repos/apt/debian/conf
```

Then, create the configuratin file named "distribution", put it into `conf` directory.

```bash
cat /var/www/repos/apt/debian/conf
Origin: Your project name
Label: Your project name
Codename: <osrelease>
Architectures: i386 amd64 source
Components: main contrib non-free
Description: Apt repository for project x
SignWith: <key-id>
```

Third, add the second configuration file named "option" at the same position with "distribution".

```bash
cat /var/www/repos/apt/debian/option
verbose
basedir /var/www/repos/apt/debian
ask-passphrase
```

# (Optional) useing package form other mirror
This can be done by reprepro using `overrides`.

For example, if you want to use package for debian's official repository.

# Links
[^1]: [https://mirrorer.alioth.debian.org/](https://mirrorer.alioth.debian.org/)
[^2]: []()