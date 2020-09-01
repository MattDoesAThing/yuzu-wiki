Currently users of AMD GPUs have two options to get decent performance on yuzu. One could use the Vulkan backend in Windows, however this comes with poor stability as yuzu's Vulkan implementation lacks proper memory management. The other option is to use the OpenGL backend in Linux with [Mesa](https://mesa3d.org/)'s open-source RadeonSI driver. Decent stability can be achieved on Linux, but the current stable version of Mesa found in most Linux distributions causes unrecoverable crashes in many games on yuzu. Some crashes are caused by an old Mesa version, and many more are caused by the old, stable version of [LLVM](https://llvm.org/) required by Mesa to compile shaders.

Most crashes are solved upstream on both Mesa and LLVM, so this is a guide about installing the latest LLVM and Mesa versions to an [Arch Linux](https://www.archlinux.org/) or [Manjaro](https://manjaro.org/) computer.

## Preparations
For this guide, either an install of Arch Linux or any distro derived from Arch Linux, such as Manjaro, is necessary to follow along. If you are a beginner with Linux, Manjaro is easier to set up and install to your computer than Arch Linux, and it can be downloaded [here](https://manjaro.org/get-manjaro/). Arch Linux can be found [here](https://www.archlinux.org/download/). General setup of the operating system is outside the scope of this guide, but here is [Manjaro's installation guide](https://manjaro.org/support/firststeps/), and here is [Arch Linux's installation guide](https://wiki.archlinux.org/index.php/Installation_guide).

Once installed, update your packages with `pacman`, the [package manager in Arch Linux](https://wiki.archlinux.org/index.php/Pacman).
```
sudo pacman -Syu
```

There are a few dependencies needed to complete this guide, as well. Run the following command to install the dependencies. If you have already followed yuzu's [Building for Linux](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Linux) guide, then this next step is unnecessary.
```
sudo pacman -S --needed git base-devel
```

## Using Chaotic-AUR to Install `llvm-git`
<!-- The following is left commented in anticipation of Arch's glibc version getting ahead of Manjaro's in the future. ->
<!-- **WARNING: Manjaro users should avoid this part of the guide for now.** Arch Linux, and Chaotic-AUR by extension, has upgraded the glibc version to 2.32, and Manjaro is still using 2.31, thus packages on Chaotic-AUR are too recent for use on Manjaro. Users should build [llvm-git](https://aur.archlinux.org/packages/llvm-git/) and [llvm-libs-git](https://aur.archlinux.org/packages/llvm-libs-git/) directly from the AUR. -->

The first step is to add the [Chaotic-AUR](https://lonewolf.pedrohlc.com/chaotic-aur/) [repository](https://wiki.archlinux.org/index.php/Unofficial_user_repositories) to your machine. This will give us access to a daily build of llvm-git (version 12.0.0 as of writing), which we need for building `mesa-git` later. Append following to the end `/etc/pacman.conf`:

```
[chaotic-aur]
# Brazil
Server = http://lonewolf-builder.duckdns.org/$repo/x86_64
# Germany
Server = http://chaotic.bangl.de/$repo/x86_64
# USA (Cloudflare proxy)
Server = https://repo.kitsuna.net/x86_64
```

This can be done so by opening `/etc/pacman.conf` in your terminal with a [text editor](https://wiki.archlinux.org/index.php/List_of_applications#Text_editors), i.e.
```
sudo nano /etc/pacman.conf
```
Then copy the repository information into the editor. It is suggested to move the URL of the closest server to the top of this list.

Since Chaotic-AUR is a signed repository, its keys need to be added and signed:
```
sudo pacman-key --keyserver hkps://hkps.pool.sks-keyservers.net -r 3056513887B78AEB 8A9E14A07010F7E3
sudo pacman-key --lsign-key 3056513887B78AEB
sudo pacman-key --lsign-key 8A9E14A07010F7E3 
```

Afterwards, update your package lists and packages:
```
sudo pacman -Syu
```

LLVM will be installed later automatically when `mesa-git` is being built. This section was just setup to make that happen later.

Chaotic-AUR provides access to many packages, including `mesa-tkg-git` and `mesa-aco-git`. **Do not install Mesa from Chaotic-AUR.** These packages are updated daily, and while there is nothing wrong with them in their own right, they use LLVM stable (version 10) which is not suitable for yuzu.

## Installing `mesa-git`
The next step is building Mesa from source. Clone the [`mesa-git`](https://aur.archlinux.org/packages/mesa-git/) build script from the [Arch User Repository](https://wiki.archlinux.org/index.php/Arch_User_Repository):
```
git clone https://aur.archlinux.org/mesa-git.git
```
Then change the working directory over to the newly cloned directory:
```
cd mesa-git
```
This gives us a [`PKGBUILD`](https://wiki.archlinux.org/index.php/PKGBUILD), a script that helps us build a package (hence the name).

In order to use the daily version of LLVM from Chaotic-AUR, the [environment variable](https://wiki.archlinux.org/index.php/Environment_variables) `MESA_WHICH_LLVM` needs to be set to `3`. Without it, `mesa-git` is configured to build with the stable version of LLVM. Run [`makepkg`](https://wiki.archlinux.org/index.php/Makepkg) from inside the `mesa-git` directory to build and install Mesa:
```
MESA_WHICH_LLVM=3 makepkg -si
```

`makepkg` will run `pacman` during the install and require credentials. It will ask to install `llvm-git`, `llvm-libs-git`, and `clang-git` over `llvm`, `llvm-libs`, and `clang`, respectively. Press `y` and hit `ENTER` to allow it to do so for each package. `mesa-git` should take a while to build.

Once it has finished building, it may ask for credentials again. `pacman` will ask to replace more packages. Press `y` and hit `ENTER` to allow it to replace these with `mesa-git`. Once `pacman` finishes installing it, `mesa-git` should be installed. Restart your machine to let all the changes take effect.

### Verify the Installation
To verify that the build was successful, run `glxinfo` in the terminal and watch the LLVM version in your renderer string:
```
glxinfo | grep "OpenGL renderer"
```
The command output should be similar to this, adjusted for your own graphics card:
```
OpenGL renderer string: AMD Radeon (TM) R5 340 (OLAND, DRM 3.37.0, 5.7.12-arch1-1, LLVM 12.0.0)
```
Of particular note is the LLVM version. If it is greater than or equal to 12.0.0, then the installation was successful.

### Updating `mesa-git`
After a some time has passed, improvements to Mesa will happen upstream and become available. Updating `mesa-git` requires ensuring the `PKGBUILD` is updated and then running `makepkg` again.

Ensure the `PKGBUILD` is updated:
```
cd mesa-git
git pull
```
Then run `makepkg` again:
```
MESA_WHICH_LLVM=3 makepkg -si
```

### Optional: Prevent `pacman` From Updating `mesa-git` Automatically
Though `mesa-git` is now installed, running `sudo pacman -Syu` right now will overwrite the package with one from a repository (likely `mesa-aco-git` from Chaotic-AUR). To prevent this, `pacman` needs to ignore that package for updates. Edit the `IgnorePkg` line in `/etc/pacman.conf`:
```
#IgnorePkg   =
```
Add `mesa-git` to this list and remove the comment marker `#` if need be:
```
IgnorePkg   = mesa-git
```
Use commas to separate multiple package names if other packages are already listed there.

It is important to note this will freeze the `mesa-git` version. This means if other packages update around it, then the installed `mesa-git` version may become incompatible with the rest of the system. Update `mesa-git` from time-to-time following the guide above.

## Conclusion
yuzu will be much more stable on an AMD GPU now with the updated Mesa and LLVM versions. Some games cannot be helped for now, like crashes in Fire Emblem: Three Houses or rendering issues in Pokemon: Sword/Shield, but most other games will crash far less frequently. Any concerns/questions had in this guide can be discussed on the [yuzu forum](https://community.citra-emu.org/c/yuzu-support) or in our [Discord server](https://discord.gg/u77vRWY).
