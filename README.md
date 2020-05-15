# Thor96 Yocto BSP

To get the BSP you need to have `repo` installed and use it as:

Install the `repo` utility:

```
$: mkdir ~/bin
$: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$: chmod a+x ~/bin/repo
```

Download the BSP source:

```
$: PATH=${PATH}:~/bin
$: mkdir boundary-bsp
$: cd boundary-bsp
$: repo init -u git@github.com:rosterloh/oe-manifest.git -b thor96
$: repo sync
```

At the end of the commands you have every metadata you need to start work with.

To start a simple image build:

```
$: source ./setup-environment build
$: bitbake core-image-minimal
```

You can use any directory to host your build.

The source code is checked out at `sources`.