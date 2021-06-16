## Intel

For recent versions of distros such as Ubuntu 20.04 and Fedora 32, the default installed version of Mesa provided by the distro is recommended, running the Iris driver and ANV for Vulkan. For older versions such as Ubuntu 18.04, Linux Mint 19.3, Debian Buster, RHEL 8, and others, users are likely to run in to some issues (issues that have yet to be reported for yuzu specifically, but be advised). For now as a cautionary measure, here are some recommendations:

- Ubuntu 20.04, 20.10, Linux Mint 20, Debian Bullseye: The stable version of Mesa is recommended.
    - Optionally, users can install Kisak's Mesa PPAs (see below).
- Ubuntu 18.04, Linux Mint 19: Install [Kisak's Mesa Fresh PPA](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa):
    - Debian Buster users can try this, but there's been no investigation to confirm that this works well on the distribution. Install the PPA at your own risk.
    - **Don't forget to use HWE X and kernel or equivalent** [[source](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa)] [[link](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)].

```
sudo add-apt-repository ppa:kisak/kisak-mesa
sudo apt-get update
sudo apt-get dist-upgrade
```

- Fedora 32, 33, Rawhide: The stable version of Mesa is recommended.
    - Optionally, users can install the [AMD](#amd) recommendation for Fedora 32.
- RHEL 8 and equivalent: No confirmed solution. Users can try manually building Mesa, installing it to an alternate root location, and setting the variables `LD_LIBRARY_PATH` and `LIBGL_DRIVERS_PATH` appropriately, but this has not been confirmed to work.
- Arch Linux and Manjaro: The default version of Mesa is recommended. For Vulkan, install `vulkan-intel`.
    - (Optional) Enable [mesa-git](https://wiki.archlinux.org/index.php/Unofficial_user_repositories#mesa-git) unofficial repository your machine, then install `mesa-git`  and `vulkan-intel-git`.
        - Users who have not setup multilib can safely skip 32-bit packages.
        - Don't forget to add `SigLevel = PackageOptional` when you enable the `mesa-git` repository.

## NVIDIA

The latest available proprietary NVIDIA blob in the package manager is recommended. Drivers older than the 450 series may not be compatible with Linux 5.8 and above. Aside from this, users should expect a similar yuzu experience to that found on Windows, as the drivers are nearly identical.

- Ubuntu and Linux Mint: Install the latest available NVIDIA driver:
    - Mint 20, Ubuntu 18.04 and Ubuntu 20.04 should use `nvidia-driver-440` for now until the newer drivers are compatible with the older kernel versions.
    - Ubuntu 20.10 and later can use `nvidia-driver-450`.
- Debian: See the [their wiki page](https://wiki.debian.org/NvidiaGraphicsDrivers) to install the most recent NVIDIA driver available for your graphics card.
- Fedora, RHEL and equivalent like CentOS: Enable [RPM Fusion](https://rpmfusion.org/Configuration) (at least **nonfree**), update, then install `xorg-x11-drv-nvidia`
    - RPM Fusion free is needed to install FFmpeg libraries for yuzu, so both will need to be enabled anyway.
- Arch Linux: Depending on your needs, install either `nvidia` or `nvidia-dkms` in pacman
- Manjaro: Use Manjaro Settings Manager -> Hardware Configuration -> Auto Install Proprietary Driver

## AMD

Mesa compiled with at least LLVM 11 is recommended to use RadeonSI. yuzu's OpenGL shader decompiler generates shaders that are often incompatible with Mesa based on LLVM 10, resulting in frequent unrecoverable driver crashes. Using a version of Mesa built on LLVM 11 or later can circumvent most of this, but for games that already cause yuzu to generate invalid shaders (e.g. Fire Emblem: Three Houses), crashes will still occur.

The recommended Vulkan driver is Mesa's RADV driver on either LLVM or ACO (the installed version's default is recommended). [AMDVLK](https://github.com/GPUOpen-Drivers/AMDVLK) also works okay in most scenarios, but can be a bit slower and has notable bugs in some games like Super Smash Bros. Ultimate. These drivers can be installed simultaneously and selected in yuzu at runtime, so the user can compare the two if they wish.

- Ubuntu 20.10 and later, Debian Bullseye: The stable version of Mesa is recommended.
    - Update the machine if it has not been recently: the LLVM version has updated to 11 and is now sufficient to run yuzu.
    - Optionally, users can install Kisak's Mesa PPAs (see below).
- Ubuntu 18.04 and 20.04, Linux Mint 19 and 20: Install [Kisak's Mesa Fresh PPA](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa) (frequent builds of Mesa using LLVM 11)
    - Debian Buster users can try this, but there's been no investigation to confirm that this works well on the distribution. Install the PPA at your own risk.
    - **Don't forget to use HWE X and kernel or equivalent** [[source](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa)] [[link](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)].

```
sudo add-apt-repository ppa:kisak/kisak-mesa
sudo apt-get update
sudo apt-get dist-upgrade
```

- Fedora 33, Rawhide: The stable version of Mesa is recommended.
    - Optionally, users can install the following recommendation for Fedora 32.
- Fedora 32: Enable and install [Che's Mesa COPR](https://copr.fedorainfracloud.org/coprs/che/mesa/) (daily builds of Mesa git using LLVM 12):

```
sudo dnf copr enable che/llvm
sudo dnf copr enable che/mesa
sudo dnf update
```

- RHEL 8 and equivalent: No confirmed solution. Users can try manually building Mesa and LLVM 11, installing them to an alternate root location, and setting the variables `LD_LIBRARY_PATH` and `LIBGL_DRIVERS_PATH` appropriately, but this has not been confirmed to work.
- Arch Linux and Manjaro: The stable version of Mesa is recommended. For Vulkan, install `vulkan-radeon`.
    - Update the machine if it has not been recently: the LLVM version has updated to 11 and is now sufficient to run yuzu.
    - (Optional) Enable [mesa-git](https://wiki.archlinux.org/index.php/Unofficial_user_repositories#mesa-git) unofficial repository, then install `mesa-git`  and `vulkan-radeon-git` (frequent builds of Mesa git using LLVM 12).
        - Users who have not setup multilib can safely skip 32-bit packages.
        - Don't forget to add `SigLevel = PackageOptional` when you enable the `mesa-git` repository.

## Environment Variables

Some environment variables are needed to fix certain graphical issues in yuzu or increase performance. A variable can be used simply by pre-pending the command with the needed variables. For example, to play Kirby on AMD:

```
force_integer_tex_nearest=true ./yuzu
```

### NVIDIA

- `__GL_THREADED_OPTIMIZATIONS=1` can net additional performance.

### AMD

- `force_integer_tex_nearest=true` fixes black textures in Kirby Fighters 2 and Kirby Star Allies.
- `AMD_DEBUG=nohyperz` fixes black textures in The Legend of Zelda: Breath of the Wild and both Xenoblade Chronicles games for GCN ≥ 4.0 GPUs.
- `mesa_glthread=true` can net additional performance, but only if the executable is not named `yuzu`. Otherwise, this variable already defaults to `true` for executables named `yuzu`, so it may not be necessary.

## Notes

- Mesa supports OpenGL 4.6 for Intel Gen 8 GPUs (Broadwell, Gen 5 CPUs) when using the (now default) Iris driver. yuzu will not work with the older i965 driver.
- Users looking to build Mesa on Arch Linux themselves can follow the [old guide](https://github.com/yuzu-emu/yuzu/wiki/%5BDeprecated%5D-Building-Mesa-on-Arch-Linux).

## Pitfalls

- Using nouveau (Mesa) with NVIDIA is not recommended. Since the [Texture Cache Rewrite](https://github.com/yuzu-emu/yuzu/pull/4967) was merged, games have been booting on nouveau. However, almost all games, especially those that require 3D rendering, have some sort of issues.
- Do not use AMDGPU-PRO. :)
    - AMDGPU-PRO is fine to use for most of its features (OpenCL, AMF, Vulkan to some extent), but it is *strongly* recommended not to install its libGL component.
