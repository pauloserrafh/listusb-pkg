# listusb-pkg

Debian package for (listusb)[https://github.com/sergioprado/listusb]


## Install
To install, only the `.deb` file is required

### Download the .deb installer
`wget https://github.com/pauloserrafh/listusb-pkg/raw/master/listusb_1.0-1_amd64.deb`

### Install
`dpkg -i listusb_1.0-1_amd64.deb`

## Run
`listusb`

## Build
If you want to rebuild after changing the source files:

First it is necessary to download the source tarball. On github is
possible to download as `.zip` or as `.tar.gz` if a release is created.

### Rename the source tarball
The file should be renamed to follow the pattern
`listusb_X.Y.orig.tar.gz`
*Note:*
- `X` and `Y` are the version indicators
- `.orig`is required before the `.tar.gz` extension.
- The separator from package name and version is lodash `_`

### Extract the source tarball
Extract the source tarball in a folder with the patern
`listusb-X.Y`
*Note:*
- The separator from package name and version is `-`
- `X` and `Y` are the version indicators

### Create initial package
- Move to the extracted directory
`cd listusb-X.Y`

- Create the initial package
`dh_make`

- (Optional) Remove *.ex and *.EX files
`rm *.ex *.EX`

### Update debian/rules
To have the package properly installed, it is necessary to have it 
properly installed at /usr/bin.
Add the following lines to the newly created `debian/rules` file
```
override_dh_auto_install:
	install -D -m 0755 listusb $$(pwd)/debian/listusb/usr/local/bin/listusb
```
*Note:*
The file follows the makefile sintax so it is required that the second
line is idented with tabs and *NOT* spaces.

### Run debuild
This is what actually creates the `.deb` package
`debuild -us -uc`

Now you have an `.deb` file that can be installed using `dpkg`.
See the references to learn how to publish on an ubuntu PPA.

## References
Check some references to learn more about building Debian packages
- (Debian PackagingIntro)[https://wiki.debian.org/Packaging/Intro]
- (Debian Building Tutorial)[https://wiki.debian.org/BuildingTutorial]
- (Using dh-make to prepare debian packages)[https://blog.packagecloud.io/eng/2015/07/14/using-dh-make-to-prepare-debian-packages/]
- (Building debian packages with debuild)[https://blog.packagecloud.io/debian/debuild/packaging/2015/06/08/buildling-deb-packages-with-debuild/]
- (HOWTO: Build debian packages for simple shell scripts)[https://blog.packagecloud.io/eng/2016/12/15/howto-build-debian-package-containing-simple-shell-scripts/]
- (Building a Debian (`.deb`) source package, and publishing it on an Ubuntu PPA)[https://saveriomiroddi.github.io/Building-a-debian-deb-source-package-and-publishing-it-on-an-ubuntu-ppa/]