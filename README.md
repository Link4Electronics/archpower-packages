# archpower-packages
Packages for ArchPOWER

* PowerPC 64-bit big-endian ELFv2 platform
* PowerPC 64-bit little-endian ELFv2 platform (didn't test most of them since don't have a PPC64LE system)
* PowerPC 32-bit platform
* PowerPC 32-bit with AltiVec (G4 only, a repo named `altivec` for packages compiled with -mcpu=7400 -mabi=altivec)
* PowerPC 32-bit with SMP (Wii U espresso, although I don't own a Wii U so have no idea if the packages will work)

Compiled some packages against `[testing]`

## Usage
Adding to pacman.conf (will arrange signature later)
```
[extrappc-any]
SigLevel = Never
Server = https://raw.githubusercontent.com/Link4Electronics/archpower-packages/main/extrappc/any

[extrappc]
SigLevel = Never
Server = https://raw.githubusercontent.com/Link4Electronics/archpower-packages/main/extrappc/$arch
```

`sudo pacman -Syu`

How to manually install:

`sudo pacman -U <package-name>.zst`

lua-filesystem requires to use luarocks to install

`sudo luarocks install <package-name>.rock`

[Mirror](https://archive.org/details/linuxppc64compiled) containing large compiled packages due 100MB microsoft github size limit for free accounts


Command to update repo: repo-add extrappc.db.tar.zst *.pkg.tar.zst

## Caveats
**I make no commitment to update these in the future**

* `doom64ex-plus` - requires `DOOM64.WAD` `doom64ex-plus.wad` `DOOMSND.DLS` and `Doom64.kpf` copied to `~/.local/share/doom64ex-plus`
* `ecwolf` - need all `*.WL6` assets and `ecwolf.pk3` on same folder `~/.config/ecwolf,` open a terminal in this folder and type `ecwolf`
* `eduke32, nblood, pcexhumed, rednukem` requires `gtk2` to have a launcher
* `fceux` - Use `SDL` as video driver instead of `OpenGL`
* `ioquake3` - Need to copy `q3config.cfg` from game disk to `~/.local/share/Quake3/baseq3`
* `nxengine-evo` - no sfx, only music, `CSE2EX` works fine
* `snes9x-gtk` - On PPC32, you may need to change `HardwareAcceleration` line in `~/.config/snes9x/snes9x.conf` to `xv` or something else, otherwise it doesn't start
* `2s2h` - Zelda Majora's Mask, generate `mm.o2r` asset from a x86_64 PC using `2s2h 1.0.1`, move `mm.o2r`to `~/.local/share/2ship/`
* `soh` - Zelda Ocarina of Time, generate  `oot.o2r` `oot-mq.o2r` assets from a x86_64 PC using `SoH 9.1.1`, move them to `~/.local/share/soh/` (only had lucky with european gamecube)
* `spaghettikart` - Mario Kart 64, generate `mk64.o2r` asset from a x86_64 PC using `SK 0.9.9.1`, move to `~/.local/share/spaghettify/`
* `starship-sf64` - Star Fox 64, generate `sf64.o2r` asset from a x86_64 PC using `Starship 2.0.0`, move to `~/.local/share/ship/`
* `vice` - There's no icon, start from console with `x64`
* `wargus` and `war1gus` - Warcraft I & II, generate assets on x86_64 PC using `Stratagus 3.3.2` with respective game and place them at `~/.local/share/stratagus/data.War1gus` or `~/.local/share/stratagus/data.Wargus`
* `xash3d-fwgs` - Half-Life port, need to compile [Half-Life SDK](https://github.com/FWGS/hlsdk-portable) and place them at `~/.xash3d/valve/dlls/hl_ppcXX.so` and `~/.xash3d/valve/cl_dlls/client_ppcXX.so`. Game assets inside `~/.xash3d/valve`
* `yamagi-quake2` - Quake 2, edit `~/.yq2/baseq2/config.cfg` change `vid_renderer` to `gl1` and change sound backend to `SDL` from main menu

# Issues
* `eduke32, rednukem` - Duke Nukem 3D has no MIDI music, `rednukem` Duke Nukem 64 sound is messed up, Ion Fury crashes when going to menu [issue](https://voidpoint.io/terminx/eduke32/-/issues/325)
* `mesa` - Mesa drivers has swapped colors for some pixelformats like RGBA5551 RGBA4444 etc, and AMD Radeon GPUS like CAICOS has ring 5 UVD3.1 issue so no hwaccel for videos and ring0 on U4 CPC945 pcie x16 slot
* `planetblupi` When try to run says can't find cdrom, probably byteswap issues with game data, Construction mode works [issue](https://github.com/blupi-games/planetblupi/issues/119)
* `SDLPop` - Prince of Persia flashes `blue` instead of `bright yellow` when grab the sword or dies. When get hit flashes `blue` too instead of `red` [issue](https://github.com/NagyD/SDLPoP/issues/185)
* `sm64ex and forks` - DynOS doesn't work and can't provide package since requires ROM during building
* `soh` - Zelda Ocarina of Time has only music, sound effects are muted [issue](https://github.com/HarbourMasters/Shipwright/issues/4513)
* `2s2h` - Zelda Majora's Mask has no sound [issue](https://github.com/HarbourMasters/2ship2harkinian/issues/802)
* `spaghettikart` - Mario Kart 64 has no sound
* `starship-sf64` - Starfox 64 has no sound

 PowerPC32
* `kernel` there's issue with `io_uring` that makes `cmake` unstable
* `ecwolf` `etlegacy` `dhewm3` `clownmdemu` `supertux` had issues in PPC32, `ecwolf` hangs when going to menu and render issues, `dhewm3` wrong colors, `clownmdemu` hangs, `supertux` render issues

## Couldn't pack or had issues packaging
`dethrace` `dRally` `bermuda` `raptor` `stuntcarremake` `supermariowar` They're at [archive.org](https://archive.org/details/linuxppc64compiled) repo

# Minecraft
Minecraft works up to `1.12.2`, which is last version that supports `LWJGL2` and `Java 8`

Version `1.8.1` is last version that renders main menu properly, `1.8.2 and up`  has graphical issues in main menu but in-game is fine, better than nothing

## Steps
Only tested on `PPC64` and will assume this arch for guide, don't know about `PPC32` but probably works

For this guide will use `~/Downloads` as folder for console commands, you can change it to your liking
* Install `jre8-openjdk`, one of these launchers `multimc` or `primslauncher` and their dependecies
* Download `Minecraft XX-bit libs.7z` according to your platform and extract it to `~/Downloads`
* `sudo cp ~/Downloads/liblwjgl.so /usr/lib/jvm/java-8-openjdk/jre/lib/ppc64` (adapt for ppc32 here)
* Open MultiMC or Prism Launcher, Add Instance, chose version 1.12.2 or below, Edit Instance, LWJGL 2 Change version to `2.9.1` (last version that works)
* Go to Settings, Custom commands, check Custom Commands and paste in Wrapper command: `sh -c "cp ~/Downloads/codecjorbis-1.0-SNAPSHOT.jar ../../../libraries/com/paulscode/codecjorbis/*/*.jar; exec $INST_JAVA \"$@\""` This library is used to fix audio in big-endian machines
* Suggest to install a loader, go to Version, Install Loader, choose `Forge` and install `Relictium` to help a little bit with performance, but it swaps some colors ingame
* Enjoy the game!

# ANY repo
An example to add to `pacman.conf`, since it's `any`, it's easier to just download from an official `Arch repo` so don't have to compile it. 
```
[core]
SigLevel = Never
Server = https://archlinux.c3sl.ufpr.br/core/os/x86_64

[extra]
SigLevel = Never
Server = https://archlinux.c3sl.ufpr.br/extra/os/x86_64
```
List of `any` packages used so far:
`blueprint-compiler` `extra-cmake-modules` `fpc-src (for lazarus)` `freepats-general-midi` `fs-uae-launcher` `kicad-library` `luarocks` `openttd-opengfx` `openttd-opensfx` `python-kikit` `python-pcbnewtransition` `python-tmdbsimple` `soundfont-fluid` `unicode-character-database`

Mate:
`icon-naming-utils` `mate-backgrounds` `mate-common` `mate-icon-theme` `mate-icon-theme-faenza` `mate-themes` `mate-user-guide` `mathjax2` `mozo`

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
* [ReDave](https://github.com/kodi-redave) - For PPC64 Minecraft libraries
* [techflashYT](https://github.com/techflashYT) - For package repository and Xbox 360 kernel contributions
* [UnknownShadow200](https://github.com/UnknownShadow200) - For fixing ClassiCube for PPC64
* [vasi](https://github.com/vasi) - For PowerPC linux kernel contributions, guide and packages repository

[ArchPOWER discord community](https://discord.gg/HntKjSTrVe).

# Fair Use Disclaimer
The content provided on this repository is for informational and educational purposes only. It is not intended to infringe upon any copyrighted material.

If you believe that any content on this repository violates your copyright or intellectual property rights, please contact us immediately to seek resolution.

I am not liable for any loss or damage, including but not limited to indirect or consequential loss or damage, arising from the use of or reliance on any content found on this repository.
