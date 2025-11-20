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

* **I make no commitment to update these in the future**

* [ecwolf] - need all `*.WL6` assets and `ecwolf.pk3` on same folder `~/.config/ecwolf,` open console in this folder and type `ecwolf`
* [eduke32, nblood, pcexhumed, rednukem] requires `gtk2` to have a launcher (it's not considered as a dependency when making the project)
* [2s2h] - Zelda Majora's Mask, generate `mm.o2r` and `2ship.o2r` assets from a x86_64 PC using `2s2h 1.0.1`, move `mm.o2r`to `~/.local/share/2ship/` and with `sudo` replace `2ship.o2r` in `/opt/2s2h/`
* [soh] - Zelda Ocarina of Time, generate  `oot.o2r` `oot-mq.o2r` assets (need `soh.o2r` too) from a x86_64 PC using `SoH 9.1.1`, move them to `~/.local/share/soh/` (only had lucky with european gamecube)
* [spaghettikart] - Mario Kart 64, generate `mk64.o2r` asset from a x86_64 PC using `SK 0.9.9.1`, move to `~/.local/share/spaghettify/`

# Issues
* [dethrace] - Carmageddon has issues in PPC64, works fine in PPC32 (but can't compile in PPC32 due to `io_uring` causing issues with `cmake`)
* [mesa] - Mesa drivers has swapped colors for some pixelformats like RGBA5551 RGBA4444 etc and issues with float FP16 as concluded [here](https://gitlab.freedesktop.org/mesa/mesa/-/issues/13954), radeon r600g has no H.264 acceleration [issue](https://gitlab.freedesktop.org/mesa/mesa/-/issues/588)
* [nestopia] Has inverted colors, already tried [this](https://github.com/0ldsk00l/nestopia/issues/25) solution but didn't work so removed from repo
* [planetblupi] When try to run says can't find cdrom, probably byteswap issues with game data, Construction mode works
* [SDLPop] - Prince of Persia flashes `blue` instead of `bright yellow` when grab the sword or dies. When get hit flashes `blue` too instead of `red` [issue](https://github.com/NagyD/SDLPoP/issues/185)
* [sm64ex and forks] - DynOS doesn't work and can't provide package since requires ROM during building
* [soh] - Zelda Ocarina of Time has only music, sound effects are muted [issue](https://github.com/HarbourMasters/Shipwright/issues/4513)
* [2s2h] - Zelda Majora's Mask has no sound [issue](https://github.com/HarbourMasters/2ship2harkinian/issues/802)
* [spaghettikart] - Mario Kart 64 has no sound
* [starship] - Starfox 64 has no sound

 PowerPC32
* [kernel] there's issue with `io_uring` that makes cmake unstable

# Minecraft

Minecraft works up to `1.12.2`, which is last version that supports `LWJGL2` and `Java 8`

## Steps

Only tested on `PPC64` and will assume this arch for guide, don't know about `PPC32` but probably works
* Install `jre8-openjdk`, one of these launchers `multimc-git` or `primslauncher-offline` and their dependecies
* Download `Minecraft XX-bit libs.7z` according to your platform and extract it to `~/Downloads`, for this guide will use `~/Downloads` as folder for console commands
* `sudo cp ~/Downloads/liblwjgl.so /usr/lib/jvm/java-8-openjdk/jre/lib/ppc64` (adapt for ppc32 here)
* Open MultiMC or Prism Launcher, Add Instance, chose version 1.12.2 or below, Edit Instance, LWJGL 2 Change version to `2.9.1` (last version that works)
* Go to Settings, Custom commands, check Custom Commands and paste in Wrapper command: `sh -c "cp ~/Downloads/codecjorbis-1.0-SNAPSHOT.jar ../../../libraries/com/paulscode/codecjorbis/*/*.jar; exec $INST_JAVA \"$@\""` This library is used to fix audio in big-endian machines
* Suggest to install a loader, go to Version, Install Loader, choose Forge and install `Relictium` to help a little bit with performance, but it swaps some colors ingame, I suspect this mod changes RGBA8888 32-bit textures to something 16-bit and causes the colors to change
* That's it, enjoy!
