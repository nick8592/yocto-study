# Yocto Study
 - [Yocto Homepage](https://github.com/nick8592/yocto-study.git)

# Setup Environment
Use docker image
```bash
docker pull ubuntu:20.04
```
Check update
```
apt update
apt upgrade
apt install sudo
```
# Build Host Packages ([link](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html#build-host-packages))
```bash
sudo apt install build-essential chrpath cpio debianutils diffstat file gawk gcc git iputils-ping libacl1 liblz4-tool locales python3 python3-git python3-jinja2 python3-pexpect python3-pip python3-subunit socat texinfo unzip wget xz-utils zstd
```
# Use Git to Clone Poky ([link](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html#use-git-to-clone-poky))
```bash
cd home/
git clone https://git.yoctoproject.org/poky

Cloning into 'poky'...
remote: Enumerating objects: 683895, done.
remote: Counting objects: 100% (2081/2081), done.
remote: Compressing objects: 100% (395/395), done.
remote: Total 683895 (delta 1787), reused 1824 (delta 1685), pack-reused 681814
Receiving objects: 100% (683895/683895), 216.16 MiB | 860.00 KiB/s, done.
Resolving deltas: 100% (496719/496719), done.
```
