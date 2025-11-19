## archpower-packages

Packages for ArchPOWER

For now only powerpc64 (big-endian) and powerpc 32-bit (compiled with linux-g4 kernel) platform

## Usage

Adding to pacman.conf (I know it s*cks without signature, but "it is what it is")
```
[extra-any]
SigLevel = Never
Server = https://raw.githubusercontent.com/Link4Electronics/archpower-packages/main/extra/any

[extra]
SigLevel = Never
Server = https://raw.githubusercontent.com/Link4Electronics/archpower-packages/main/extra/$arch
```

`sudo pacman -Syu`

How to manually install:

`sudo pacman -U <package-name>.zst`

lua-filesystem requires to use luarocks to install

`sudo luarocks install <package-name>.rock`

Mirror and containing large compiled packages: https://archive.org/details/linuxppc64compiled

## Caveats

* I make no commitment to update these in the future
* [ecwolf] - need all `*.WL6` assets and `ecwolf.pk3` on same folder `~/.config/ecwolf,` open console in this folder and type 'ecwolf'
* [soh] - Zelda Ocarina of Time, generate  `oot.o2r` `oot-mq.o2r` assets (need `soh.o2r` too) from a x86_64 PC using `SoH 9.1.1`, move them to `~/.local/share/soh/`
* [spaghettikart] Mario Kart 64, generate `mk64.o2r` asset from a x86_64 PC using `SK 0.9.9.1`, move to `~/.local/share/spaghettify/`
