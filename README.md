# archpower-packages

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
* [ecwolf] - need all `*.WL6` assets and `ecwolf.pk3` on same folder `~/.config/ecwolf,` open console in this folder and type `ecwolf`
* [soh] - Zelda Ocarina of Time, generate  `oot.o2r` `oot-mq.o2r` assets (need `soh.o2r` too) from a x86_64 PC using `SoH 9.1.1`, move them to `~/.local/share/soh/`
* [spaghettikart] - Mario Kart 64, generate `mk64.o2r` asset from a x86_64 PC using `SK 0.9.9.1`, move to `~/.local/share/spaghettify/`

# Issues
* [mesa] - Mesa drivers has swapped colors for some pixelformats like RGBA5551 RGBA4444 etc as concluded [here](https://gitlab.freedesktop.org/mesa/mesa/-/issues/13954) and has issues with float FP16, radeon r600g has no H.264 acceleration [issue](https://gitlab.freedesktop.org/mesa/mesa/-/issues/588)
* [nestopia] Has inverted colors, already tried [this](https://github.com/0ldsk00l/nestopia/issues/25) solution but didn't work so removed from repo
* [soh] - Zelda Ocarina of Time has only music, sound effects are muted
* [2s2h] - Zelda Majora's Mask has no sound
* [starship] - Starfox 64 has no sound
* [spaghettikart] - Mario Kart 64 has no sound

## PowerPC32
* [kernel] there's issue with `io_uring` that makes cmake unstable
