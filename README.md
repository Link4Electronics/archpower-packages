# archpower-packages
Packages for ArchPOWER

For now only powerpc64 (big-endian) platform

Adding to pacman.conf:
```
[extra-any]
Server = https://github.com/Link4Electronics/archpower-packages/tree/main/extra/any

[extra]
Server = https://github.com/Link4Electronics/archpower-packages/tree/main/extra/$arch
```

`sudo pacman -Syu`

How to manually install:

`sudo pacman -U <package-name>.zst`

lua-filesystem requires to use luarocks to install

`sudo luarocks install <package-name>.rock`

Mirror and containing large packages (soon): https://archive.org/details/linuxppc64compiled
