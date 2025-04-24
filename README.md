# Yocto Study
 - [Yocto Homepage](https://github.com/nick8592/yocto-study.git)

# Setup Environment
Use docker image ([link](https://hub.docker.com/_/ubuntu/tags?name=20.04))
```bash
$ docker pull ubuntu:20.04
```
Run docker container
```
$ docker run -it ubuntu
```
Check update
```
$ apt update
$ apt upgrade
$ apt install sudo vim
```
# Build Host Packages ([link](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html#build-host-packages))
```bash
$ sudo apt install build-essential chrpath cpio debianutils diffstat file gawk gcc git iputils-ping libacl1 liblz4-tool locales python3 python3-git python3-jinja2 python3-pexpect python3-pip python3-subunit socat texinfo unzip wget xz-utils zstd
```
# Use Git to Clone Poky ([link](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html#use-git-to-clone-poky))
```
$ cd home/
$ git clone https://git.yoctoproject.org/poky
Cloning into 'poky'...
remote: Enumerating objects: 683895, done.
remote: Counting objects: 100% (2081/2081), done.
remote: Compressing objects: 100% (395/395), done.
remote: Total 683895 (delta 1787), reused 1824 (delta 1685), pack-reused 681814
Receiving objects: 100% (683895/683895), 216.16 MiB | 860.00 KiB/s, done.
Resolving deltas: 100% (496719/496719), done.
```
Go to [Releases wiki page](https://wiki.yoctoproject.org/wiki/Releases), and choose a release codename (such as Dunfell)
For this example, check out the `Dunfell` branch based on the `Dunfell` release:
```
$ git checkout -t origin/dunfell -b my-dunfell
Branch 'my-dunfell' set up to track remote branch 'dunfell' from 'origin'.
Switched to a new branch 'my-dunfell'
```

# Building Your Image ([link](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html#building-your-image))
1. **Initialize the Build Environment**: From within the `poky` directory, run the `oe-init-build-env` environment setup script to define Yocto Project’s build environment on your build host.
   ```
   $ cd poky
   $ source oe-init-build-env
   
   You had no conf/local.conf file. This configuration file has therefore been
   created for you with some default values. You may wish to edit it to, for
   example, select a different MACHINE (target hardware). See conf/local.conf
   for more information as common configuration options are commented.
   
   You had no conf/bblayers.conf file. This configuration file has therefore been
   created for you with some default values. To add additional metadata layers
   into your configuration please add entries to conf/bblayers.conf.
   
   The Yocto Project has extensive documentation about OE including a reference
   manual which can be found at:
       https://docs.yoctoproject.org
   
   For more information about OpenEmbedded see their website:
       https://www.openembedded.org/
   
   
   ### Shell environment set up for builds. ###
   
   You can now run 'bitbake <target>'
   
   Common targets are:
       core-image-minimal
       core-image-sato
       meta-toolchain
       meta-ide-support
   
   You can also run generated qemu images with a command like 'runqemu qemux86'
   
   Other commonly useful commands are:
    - 'devtool' and 'recipetool' handle common recipe tasks
    - 'bitbake-layers' handles common layer tasks
    - 'oe-pkgdata-util' handles common target package tasks
   ```
2. **Examine Your Local Configuration File**: When you set up the build environment, a local configuration file named `local.conf` becomes available in a `conf` subdirectory of the Build Directory. Nothing need to change can type `:q` to exit.
   ```
   $ cd local
   $ vim local.conf
   ```
3. **Start the Build**: Continue with the following command to build an OS image for the target
   Common targets are: core-image-minimal/core-image-sato/meta-toolchain/meta-ide-support
   ```
   $ cd poky
   $ bitbake core-image-sato
   ```
   If show error message
   ```
   ERROR:  OE-core's config sanity checker detected a potential misconfiguration.
   Either fix the cause of this error or at your own risk disable the checker (see sanity.conf).
   Following is the list of potential problems / advisories:

   Do not use Bitbake as root.
   ```
   Edit the `sanity.conf` in `poky/meta/conf/`, reference from ([stackoverflow](https://stackoverflow.com/a/64781820))
   ```
   $ cd poky/meta/conf
   $ vim sanity.conf
   ```
   Common `INHERIT += "sanity"`, modified as below 
   ```
   # Sanity checks for common user misconfigurations
   #
   # See sanity.bbclass
   #
   # Expert users can confirm their sanity with "touch conf/sanity.conf"
   BB_MIN_VERSION = "1.46.0"
   
   SANITY_ABIFILE = "${TMPDIR}/abi_version"
   
   SANITY_VERSION ?= "1"
   LOCALCONF_VERSION  ?= "1"
   LAYER_CONF_VERSION ?= "7"
   SITE_CONF_VERSION  ?= "1"
   
   # INHERIT += "sanity"
   ```
   
