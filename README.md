# archpower-packages

Packages for ArchPOWER

* PowerPC64 big-endian platform
* PowerPC32 platform (compiled running linux-g4 kernel, no clue if makes difference due to AltiVec on G4 and apps will run on eg. G3, Wii)

## Usage

Adding to pacman.conf (will arrange signature later)
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

* **I make no commitment to update these in the future**

* `ecwolf` - need all `*.WL6` assets and `ecwolf.pk3` on same folder `~/.config/ecwolf,` open console in this folder and type `ecwolf`
* `eduke32, nblood, pcexhumed, rednukem` requires `gtk2` to have a launcher (it's not considered as a dependency when making the project)
* `jazz2-native` - Jazz Jackrabbit 2 requires OpenGL 3.3, needs to run via software rendering then `MESA_LOADER_DRIVER_OVERRIDE=llvmpipe`
* `2s2h` - Zelda Majora's Mask, generate `mm.o2r` and `2ship.o2r` assets from a x86_64 PC using `2s2h 1.0.1`, move `mm.o2r`to `~/.local/share/2ship/` and with `sudo` replace `2ship.o2r` in `/opt/2s2h/`
* `soh` - Zelda Ocarina of Time, generate  `oot.o2r` `oot-mq.o2r` assets (need `soh.o2r` too) from a x86_64 PC using `SoH 9.1.1`, move them to `~/.local/share/soh/` (only had lucky with european gamecube)
* `spaghettikart` - Mario Kart 64, generate `mk64.o2r` asset from a x86_64 PC using `SK 0.9.9.1`, move to `~/.local/share/spaghettify/`
* `starship-sf64` - Star Fox 64, generate `sf64.o2r` asset from a x86_64 PC using `Starship 2.0.0`, mote to `~/.local/share/ship/`

# Issues
* `dethrace` - Carmageddon has issues in PPC64, works fine in PPC32 (but can't compile in PPC32 due to `io_uring` causing issues with `cmake`)
* `eduke32, rednukem` - Duke Nukem 3D has no MIDI music, `rednukem` Duke Nukem 64 sound is messed up, Ion Fury crashes when going to menu [issue](https://voidpoint.io/terminx/eduke32/-/issues/325)
* `mesa` - Mesa drivers has swapped colors for some pixelformats like RGBA5551 RGBA4444 etc and issues with float FP16 as concluded [here](https://gitlab.freedesktop.org/mesa/mesa/-/issues/13954), radeon r600g has no H.264 acceleration [issue](https://gitlab.freedesktop.org/mesa/mesa/-/issues/588) and maybe part of the issue relies on [LLVM](https://github.com/llvm/llvm-project/issues/167102)
* `nestopia` Has inverted colors, already tried [this](https://github.com/0ldsk00l/nestopia/issues/25) solution but didn't work so removed from repo
* `planetblupi` When try to run says can't find cdrom, probably byteswap issues with game data, Construction mode works
* `SDLPop` - Prince of Persia flashes `blue` instead of `bright yellow` when grab the sword or dies. When get hit flashes `blue` too instead of `red` [issue](https://github.com/NagyD/SDLPoP/issues/185)
* `sm64ex and forks` - DynOS doesn't work and can't provide package since requires ROM during building
* `soh` - Zelda Ocarina of Time has only music, sound effects are muted [issue](https://github.com/HarbourMasters/Shipwright/issues/4513)
* `2s2h` - Zelda Majora's Mask has no sound [issue](https://github.com/HarbourMasters/2ship2harkinian/issues/802)
* `spaghettikart` - Mario Kart 64 has no sound
* `starship-sf64` - Starfox 64 has no sound
* `supertuxkart` - Swapped colors and crashes when goes to menu
* `xash3d-fwgs` - Half-Life port has physics models issues and crashes when LOADING new map, can explore using console `map c1a0` etc [issue](https://github.com/FWGS/xash3d-fwgs/pull/1466)

 PowerPC32
* `kernel` there's issue with `io_uring` that makes `cmake` unstable

# Minecraft

Minecraft works up to `1.12.2`, which is last version that supports `LWJGL2` and `Java 8`

## Steps

Only tested on `PPC64` and will assume this arch for guide, don't know about `PPC32` but probably works

For this guide will use `~/Downloads` as folder for console commands
* Install `jre8-openjdk`, one of these launchers `multimc-git` or `primslauncher-offline` and their dependecies
* Download `Minecraft XX-bit libs.7z` according to your platform and extract it to `~/Downloads`
* `sudo cp ~/Downloads/liblwjgl.so /usr/lib/jvm/java-8-openjdk/jre/lib/ppc64` (adapt for ppc32 here)
* Open MultiMC or Prism Launcher, Add Instance, chose version 1.12.2 or below, Edit Instance, LWJGL 2 Change version to `2.9.1` (last version that works)
* Go to Settings, Custom commands, check Custom Commands and paste in Wrapper command: `sh -c "cp ~/Downloads/codecjorbis-1.0-SNAPSHOT.jar ../../../libraries/com/paulscode/codecjorbis/*/*.jar; exec $INST_JAVA \"$@\""` This library is used to fix audio in big-endian machines
* Suggest to install a loader, go to Version, Install Loader, choose Forge and install `Relictium` to help a little bit with performance, but it swaps some colors ingame
* Enjoy the game!

# Credits (in alphabetical order)

* [BeWorld2018](https://github.com/BeWorld2018) - For fixing endianness on fallout1-ce, OpenLara etc
* [BSzili](https://github.com/BSzili) - For fixing lots of opensource games endianness like dethrace, dRally, ArxLibertatis etc
* [Clownacy](https://github.com/clownacy) - For the only Sega Mega Drive/Genesis emulator that works on Linux PPC
* [DanielGibson](https://github.com/DanielGibson) - For fixing dhewm3 for PPC64
* [deathkiller](https://github.com/deathkiller) - For bringing big-endian support for jazz2
* [GaryOderNichts](https://github.com/GaryOderNichts) - For 2ship2harkinian WiiU port which works on Linux PPC big-endian
* [IntriguingTiles](https://github.com/IntriguingTiles) - For xash3d-fwgs endianness fixes
* [kth5](https://github.com/kth5) - For creating, supporting and maintaining ArchPOWER distro and its community
* [Matias3149](https://github.com/Matias314) - For Minecraft guide and libraries
* ReDave - For PPC64 Minecraft libraries
* [techflashYT](https://github.com/techflashYT) - For package repository
* [UnknownShadow200](https://github.com/UnknownShadow200) - For fixing ClassiCube for PPC64
* [vasi](https://github.com/vasi) - For PowerPC linux kernel contributions, guide and packages repository

[ArchPOWER discord community](https://discord.gg/HntKjSTrVe).
