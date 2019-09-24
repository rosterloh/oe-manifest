# STM32MP1 OpenEmbedded Manifest

This project is the repo manifest of OpenSTLinux release.

## OE RPB Layers

|   Layer                 |   Description                    |
|:-----------------------:|:----------------------|
| oe-core | This is the main collaboration point when working on OpenEmbedded projects and is part of the core recipes. The goal of this layer is to have just enough recipes to build a basic system, this means keeping it as small as possible. |
| meta-oe | This layer houses many useful, but sometimes unmaintained recipes. Since the reduction in recipes to the core, meta-oe was created for everything else. There are currently approximately 650 recipes in this layer. |
| meta-qt5 | This is a cross-platform toolkit. |
| meta-clang | This layer is used to get the Clang toolchain. |
| meta-st-openstlinux | This layer provides the OpenSTLinux distribution. |
| meta-st-stm32mp | This is the board support layer for STM32MP1 boards. |
| meta-st-stm32mp-addons | BSP Layer addons for stm32mp (CubeMX Machine). |
| meta-st-scripts | Environment scripts for OpenSTLinux to use with Openembedded. |
| meta-st-stm32mpu-ai | OpenEmbedded meta layer to install AI frameworks and tools for the STM32MP1. |
| meta-st-stm32mpu-app-logicanalyser | OpenEmbedded meta layer to install logic analyser demo which includes a user interface embedded in a web page. |


## oe-manifest repository

These are the setup scripts for the OE buildsystem. If you want to (re)build packages or images for OE, this is the thing to use.
The OE buildsystem is using various components from the Yocto Project, most importantly the Openembedded buildsystem, the bitbake task executor and various application and BSP layers.

To configure the scripts and download the build metadata, do:
```
mkdir ~/bin
PATH=~/bin:$PATH

curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
Run repo init to bring down the latest version of Repo with all its most recent bug fixes. You must specify a URL for the manifest, which specifies where the various repositories included in the Android source will be placed within your working directory. To check out the current branch, specify it with -b:
```
repo init -u https://github.com/rosterloh/oe-manifest.git -b stm32mp1
```
When prompted, configure Repo with your real name and email address.

A successful initialisation will end with a message stating that Repo is initialised in your working directory. Your client directory should now contain a .repo directory where files such as the manifest will be kept.

To pull down the metadata sources to your working directory from the repositories as specified in the default manifest, run
```
repo sync
```

## Host package Dependencies

In order to successfully set up your build environment, you will need to install the following package dependencies.

**Step 1**: You will need git installed on your Linux host machine

`$ sudo apt-get install git`

**Step 2**: Visit the OpenEmbedded (Getting Started) wiki to see which distribution specific dependencies you will need

http://www.openembedded.org/wiki/Getting_started

Setting up the build environment will first search for `whiptail`, if it is not present then it will search for `dialog`. You only need one of the following packages to ensure your setup-environement runs correctly:

`$ sudo apt-get install whiptail`

or

`$ sudo apt-get install dialog`

## Setup Environment

It is recommended to use the `setup-environment` script. Among several things, it will prompt the user for the list of supported machines and distros. The setup script will also create (if they don't exsist) the local build configuration files.

To run the setup script:

    $ . setup-environment

And follow the instructions. If you already know the value for MACHINE and DISTRO, it is possible to set them as environment variables, e.g. 

    $ MACHINE=stm32mp1 DISTRO=openstlinux-weston source setup-environment

## Build an OpenSTLinux image

To build an image, you can run:

    $ bitbake st-image-weston

At the end of the build, your build artifacts will be found under `tmp-eglibc/deploy/images/MACHINE/`. 

See flashing instructions at https://wiki.st.com/stm32mpu/wiki/STM32MP15_Discovery_kits_-_Starter_Package#Image_flashing

## STM32MP15-Ecosystem-v1.0.0 release TAG: openstlinux-4.19-thud-mp1-19-02-20

See the wiki user guide for more information: https://wiki.st.com/stm32mpu/wiki/STM32MP1_Distribution_Package
