## Intel
The default installed version of Mesa provided by the distro is recommended. Users who are willing to experiment with their computer can follow the advice for AMD users below. There are *no known advantages* to updating Mesa past the stable version for Intel GPU users, so it is not recommended.

## NVIDIA
The latest available proprietary NVIDIA blob in the package manager is recommended. Drivers older than the 450 series may not be compatible with Linux 5.8 and above. CUDA is currently not working on Linux 5.9 [[source]](https://phoronix.com/scan.php?page=news_item&px=NVIDIA-Linux-5.9-Delayed) (which doesn't affect yuzu but is a consideration for someone who needs the compute capabilities of their GPU). Aside from these issues, users should expect a similar yuzu experience to that found on Windows, as the drivers are nearly identical.

- Ubuntu and Linux Mint: Install `nvidia-driver-450`
- Debian: https://wiki.debian.org/NvidiaGraphicsDrivers
- Fedora: Enable [RPM Fusion](https://rpmfusion.org/Configuration) (at least **nonfree**), update, then install `xorg-x11-drv-nvidia`
    - Note that RPM Fusion free is needed to install FFmpeg libraries for yuzu, so both will need to be enabled anyway.
- Arch Linux: Install either `nvidia` or `nvidia-dkms` in pacman
- Manjaro: Use Manjaro Settings Manager -> Hardware Configuration -> Auto Install Proprietary Driver

Setting the environment variable `__GL_THREADED_OPTIMIZATIONS=1` can net additional performance.

## AMD
Mesa compiled with at least LLVM 11 is recommended. yuzu's OpenGL shader decompiler generates shaders that are often incompatible with Mesa based on LLVM 10, resulting in frequent unrecoverable driver crashes. Using a version of Mesa built on LLVM 12 can circumvent most of this, but for games that already generate invalid shaders (e.g. FE:TH), unrecoverable crashes will still occur.

- Ubuntu (and Debian, Linux Mint, etc.): **No good solution**, but you can try [Oibaf's Mesa driver](https://launchpad.net/~oibaf/+archive/ubuntu/graphics-drivers) (daily builds of Mesa git using LLVM 10)

```
sudo add-apt-repository ppa:oibaf/graphics-drivers
sudo apt update
sudo apt upgrade
```

- Fedora: Enable and install [Che's Mesa COPR](https://copr.fedorainfracloud.org/coprs/che/mesa/) (daily builds of Mesa git using LLVM 12):

```
sudo dnf copr enable che/llvm
sudo dnf copr enable che/mesa
sudo dnf update
```

- Arch Linux and Manjaro: Enable [mesa-git](https://wiki.archlinux.org/index.php/Unofficial_user_repositories#mesa-git) unofficial repository your machine, then install `mesa-git` (daily builds of Mesa git using LLVM 12): <br>```sudo pacman -Syu mesa-git```
    - Users who have not setup multilib can safely skip 32-bit packages.
    - Don't forget to add `SigLevel = PackageOptional` when you enable the `mesa-git` repository.

Setting `force_integer_tex_nearest=true` fixes black textures in Kirby Fighters 2 and Kirby Star Allies.

Setting `AMD_DEBUG=nohyperz` fixes black textures in The Legend of Zelda: Breath of the Wild and both Xenoblade Chronicles games for GCN ≥ 4.0 GPUs.

Setting `mesa_glthread=true` can net additional performance, only if the executable is not named `yuzu`. Otherwise, this variable already defaults to `true` for executables named `yuzu`, so it may not be necessary to set here.

## Notes
- Mesa supports OpenGL 4.6 for Intel Gen 8 GPUs (Broadwell, Gen 5 CPUs) when using the (now default) Iris driver. yuzu will not work with the older i965 driver.
- Users looking to build Mesa on Arch Linux themselves can follow the [old guide](https://github.com/yuzu-emu/yuzu/wiki/%5BDeprecated%5D-Building-Mesa-on-Arch-Linux).

## Pitfalls
- Don't use nouveau (Mesa) with NVIDIA. Since the [Texture Cache Rewrite](https://github.com/yuzu-emu/yuzu/pull/4967), games have been booting on nouveau. However, almost all games, especially those that require 3D rendering, have some sort of issues.
- Do not use AMDGPU-PRO. :)
    - AMDGPU-PRO is fine to use for most of its features (OpenCL, AMF, Vulkan to some extent), but it is *strongly* recommended not to install its libGL component. 