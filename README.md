# Debian package for Maple

## Description

Debian rules to generate a Debian package for [Maple](https://www.maplesoft.com/products/Maple/) for amd64 architecture. The Maple installer `Maple*LinuxX64Installer.run` corresponding to the version in changelog has to be provided to build the package.

The generated Debian package:
- installs Maple in `/opt/maple`
- adds links to `maple` and `xmaple` executables in `/usr/bin`
- adds icon and desktop menu entry in `/usr/share`
- adds license file if provided

A license file `license.dat` has to be provided to use Maple either next to the installer in order to be included in the package or need to be added in `/opt/maple/license/` after the package is installed. To use a network license server the `license.dat` is simply:

    SERVER hostname-or-ip-of-license-server ANY 27000
    USE_SERVER


Inspired by [Maple Arch Linux PKGBUILD](https://aur.archlinux.org/packages/maple2021).

## Package build

1. Define the desired version:

        export VERSION=2022.0

2. Clone the git repository containing the packages rules in an empty directory:

        git clone -b $VERSION https://github.com/guillod/deb-maple.git maple-$VERSION
        cd maple-$VERSION

3. Put the Maple installer `Maple${VERSION}LinuxX64Installer.run` in the current directory (`maple-$VERSION`).
4. Optionally, put a `license.dat` file (network license server) in the same directory in order to include it in the package.
5. Generate the package for example with:

        debuild --no-lintian -i -b -uc -us

    or `sbuild` (note you can speed up the creation of the source archive using `--dpkg-source-opts="-Zgzip -z1"`).

## Installation

Once generated, the package `maple_$VERSION_amd64.deb` can be installed for example with:

    sudo apt install ../maple_$VERSION_amd64.deb


## Contact

For comments, issues, bug-reports and requests, please use the issue tracker of the current repository. Otherwise the principal author can be reached at:

    Julien Guillod
    julien.guillod CHEZ sorbonne-universite.fr
    https://guillod.org/
    Department of Mathematics
    Sorbonne University
    France
