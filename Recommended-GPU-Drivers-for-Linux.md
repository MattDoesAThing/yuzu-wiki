# Recommended GPU Drivers for Linux
## Intel
The default installed version of Mesa provided by the distro is recommended. Users who are willing to experiment with their computer can follow the advice for AMD users below. There are *no known advantages* to updating Mesa past the stable version for Intel GPU users, so it is not recommended.

## NVIDIA
The latest available proprietary NVIDIA blob in the package manager is recommended. Drivers older than the 450 series may not be compatible with Linux 5.8 and above. CUDA is currently not working on Linux 5.9 [[source]](https://phoronix.com/scan.php?page=news_item&px=NVIDIA-Linux-5.9-Delayed). Aside from these issues, users should expect a similar yuzu experience to that found on Windows, as the drivers are nearly identical.
- Ubuntu and Linux Mint: Install `nvidia-driver-450`
- Debian: https://wiki.debian.org/NvidiaGraphicsDriver
- Fedora: Enable [RPM Fusion](https://rpmfusion.org/Configuration) (at least **nonfree**), update, then install `xorg-x11-drv-nvidia`
- Arch Linux: Use either `nvidia` or `nvidia-dkms`
- Manjaro: Use Manjaro Settings Manager -> Hardware Configuration -> Auto Install Proprietary Driver

## AMD
Mesa compiled with LLVM 12 is recommended. yuzu's OpenGL shader decompiler generates shaders that are often incompatible with Mesa based on LLVM 10, resulting in frequent unrecoverable driver crashes. Using a version of Mesa built on LLVM 12 can circumvent most of this, but for games that already generate invalid shaders (e.g. FE:TH), unrecoverable crashes will still occur.
- Ubuntu (and Debian, Linux Mint, etc.): **No good solution**, but you can try [Oibaf's Mesa driver](https://launchpad.net/~oibaf/+archive/ubuntu/graphics-drivers) (daily builds of Mesa git using LLVM 10)
- Fedora: Enable and install [Che's Mesa COPR](https://copr.fedorainfracloud.org/coprs/che/mesa/) (daily builds of Mesa git using LLVM 12):
```
sudo dnf copr enable che/llvm
sudo dnf copr enable che/mesa
sudo dnf update
```
- Arch Linux and Manjaro: Enable [Chaotic-AUR](https://lonewolf.pedrohlc.com/chaotic-aur/) on your machine, then install `mesa-git` (daily builds of Mesa git using LLVM 12):
```
sudo pacman -Syu mesa-git
```

## Notes
- Mesa supports OpenGL 4.6 for Intel Gen 8 GPUs (Broadwell, Gen 5 CPUs) when using the (now default) Iris driver. yuzu will not work with the older i965 driver.
- Users looking to build Mesa on Arch Linux themselves can follow the [old guide](https://github.com/yuzu-emu/yuzu/wiki/%5BDeprecated%5D-Building-Mesa-on-Arch-Linux).

## Pitfalls
- Don't use nouveau (Mesa) with NVIDIA. Even on older cards, most games fail to boot on yuzu with this driver. Those games that do boot are doomed to crash after maybe a minute.
- Do not use AMDGPU PRO. :)