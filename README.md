# Install-bootsnote-legacy-in-ubuntu-22.04


## Update and upgrade repos

```
$ sudo apt update
$ sudo apt upgrade
```

## Install Boostnote

```
$ wget https://github.com/BoostIO/boost-releases/releases/download/v0.16.1/boostnote_0.16.1_amd64.deb
```
https://github.com/BoostIO/boost-releases/releases/


then run the following command
```
$ sudo dpkg -i boostnote_0.16.1_amd64.deb
```

Dependencies issues would be reported, if the following command is executed

```
$ sudo apt-get install -f
```

and if "Yes" is entered, the application will be removed.

> Note that the application may start withouth any issue despite dependencies not met

To open Boostnote go to:

`Activities -> Show Applications -> Boost Note` or just type the command `boostnote` on shell prompt.

## Deal with dependencies

### hold package for update/upgrade (blacklisted)
To avoid updating/upgrading this package

```
$ sudo apt-mark hold boostnote
```

to check the if the package has been marked/blacklisted for updates/upgrades

```
$ sudo apt-mark showhold
```

to unmark package

```
$ sudo apt-mark unhold boostnote
```

### Avoid unmet dependiencies messages

There would be some unmet dependencies reported when running `sudo apt-get install -f` command e.g. gconf-service, gconf2, gvfs-bin

To eliminate this message, go to:

```
$ cd /var/lib/dpkg
```
Edit the file

```
var/lib/dpkg $ sudo vi status
```

In this file look for the following section:

```
Package: boostnote
Status: hold ok installed
Priority: optional
Section: utils
Installed-Size: 335140
Maintainer: Junyoung Choi <fluke8259@gmail.com>
Architecture: amd64
Version: 0.16.1-1
Depends: gconf-service, gconf2, gvfs-bin, libc6, libcap2, libgcrypt11 | libgcrypt20, libgtk2.0-0, libnotify4, libnss3, libudev0 | libudev1, libxtst6, xdg-utils
Recommends: lsb-release
Suggests: gir1.2-gnomekeyring-1.0, libgnome-keyring0
Description: Boostnote
 The opensource note app for developers.
Homepage: https://boostnote.io

```

Change the line `Depends` to this:

```
Depends: libc6, libcap2, libgcrypt11 | libgcrypt20, libgtk2.0-0, libnotify4, libnss3, libudev0 | libudev1, libxtst6, xdg-utils
```

Save the changes, and finally execute twice:

```
$ sudo apt-get install -f
````
