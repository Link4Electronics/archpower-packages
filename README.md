# archpower-packages

Packages for ArchPOWER

* PowerPC64 big-endian platform
* PowerPC32 platform (compiled running linux-g4 kernel, no clue if makes difference due to AltiVec on G4 and apps will run on eg. G3, Wii)

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
* [eduke32, nblood, pcexhumed, rednukem] requires `gtk2` to open the launcher (it's not considered as a dependency when making the project)
* [2s2h] - Zemda Majora's Mask, generate `mm.o2r` asset from a x86_64 PC using `2s2h 1.0.1`, move to `~/.local/share/2ship/`
* [soh] - Zelda Ocarina of Time, generate  `oot.o2r` `oot-mq.o2r` assets (need `soh.o2r` too) from a x86_64 PC using `SoH 9.1.1`, move them to `~/.local/share/soh/` (only had lucky with european gamecube)
* [spaghettikart] - Mario Kart 64, generate `mk64.o2r` asset from a x86_64 PC using `SK 0.9.9.1`, move to `~/.local/share/spaghettify/`

# Issues
* [mesa] - Mesa drivers has swapped colors for some pixelformats like RGBA5551 RGBA4444 etc and issues with float FP16 as concluded [here](https://gitlab.freedesktop.org/mesa/mesa/-/issues/13954), radeon r600g has no H.264 acceleration [issue](https://gitlab.freedesktop.org/mesa/mesa/-/issues/588)
* [nestopia] Has inverted colors, already tried [this](https://github.com/0ldsk00l/nestopia/issues/25) solution but didn't work so removed from repo
* [SDLPop] - Prince of Persia flashes `blue` instead of `bright yellow` when grab the sword or dies. When get hit flashes `blue` too instead of `red` [issue](https://github.com/NagyD/SDLPoP/issues/185)
* [soh] - Zelda Ocarina of Time has only music, sound effects are muted
* [2s2h] - Zelda Majora's Mask has no sound
* [spaghettikart] - Mario Kart 64 has no sound
* [starship] - Starfox 64 has no sound
* [sm64ex and forks] - DynOS doesn't work and can't provide package since requires ROM during building

 PowerPC32
* [kernel] there's issue with `io_uring` that makes cmake unstable

# Minecraft

Minecraft works up to `1.12.2`, which is last version that supports `LWJGL2` and `Java 8`

## Steps
