**This article was written for developers. Users looking to simply run yuzu should try downloading [Mainline](https://yuzu-emu.org/downloads/) first. As it is an AppImage, it only needs to be downloaded and made executable to use it.**

***

### Dependencies

You'll need to download and install the following to build yuzu:

  * [GCC](https://gcc.gnu.org/) v11+ (for C++20 support) & misc
    * This page is being updated as we transition to GCC 11
  * If GCC 12 is installed, [Clang](https://clang.llvm.org/) v14+ is required for compiling
  * [CMake](https://www.cmake.org/) 3.15+

The following are handled by yuzu's externals:

  * [FFmpeg](https://ffmpeg.org/)
  * [SDL2](https://www.libsdl.org/download-2.0.php) 2.0.18+

If version 5.15.2 is not already installed, pre-compiled binaries for Qt 5.15.2 will be downloaded from [here](https://github.com/yuzu-emu/ext-linux-bin) automatically by CMake:

  * [Qt](https://qt-project.org/downloads) 5.15+

All other dependencies will be downloaded by [Conan](https://conan.io/downloads.html) if needed:

  * [Boost](https://www.boost.org/users/download/) 1.73.0+
  * [Catch2](https://github.com/catchorg/Catch2)
  * [fmt](https://fmt.dev/)
  * [lz4](http://www.lz4.org)
  * [nlohmann_json](https://github.com/nlohmann/json)
  * [OpenSSL](https://www.openssl.org/source/)
  * [opus](https://opus-codec.org/downloads/)
  * [ZLIB](https://www.zlib.net/)
  * [zstd](https://facebook.github.io/zstd/)

Dependencies are listed here as commands that can be copied/pasted. Of course, they should be inspected before being run.

- Arch / Manjaro:
  - `sudo pacman -Syu --needed base-devel boost catch2 cmake ffmpeg fmt git glslang libzip lz4 mbedtls ninja nlohmann-json openssl opus python-pip python2 qt5 sdl2 zlib zstd`
  - `python3 -m pip install --user conan`
  - Building with QT Web Engine needs to be specified when running Cmake with the param `-DCMAKE_CXX_FLAGS="-I/usr/include/qt/QtWebEngineWidgets"` with qt5-webengine installed.
  - GCC 10 or later is required.
- Ubuntu / Linux Mint / Debian:
  - `sudo apt-get install autoconf cmake g++-10 gcc-10 git glslang-tools libasound2 libboost-context-dev libglu1-mesa-dev libhidapi-dev libpulse-dev libtool libudev-dev libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0 libxcb-xinerama0 libxcb-xkb1 libxext-dev libxkbcommon-x11-0 mesa-common-dev nasm ninja-build python3 python3-pip qtbase5-dev qtbase5-private-dev qtwebengine5-dev libmbedtls-dev`
  - `pip3 install --user conan`
  - Ubuntu 20.04, Linux Mint 20, or Debian Bullseye or later is required.
  -  Users need to manually specify building with QT Web Engine enabled.  This is done using the parameter `-DYUZU_USE_QT_WEB_ENGINE=ON` when running CMake. 
  - Users need to manually specify building with GCC 10. This can be done by adding the parameters `-DCMAKE_C_COMPILER=gcc-10 -DCMAKE_CXX_COMPILER=g++-10` when running CMake. i.e.
  - Users need to manually disable building SDL2 from externals if they intend to use the version provided by their system by adding the parameters `-DYUZU_USE_EXTERNAL_SDL2=OFF`

```
cmake .. -GNinja -DCMAKE_C_COMPILER=gcc-10 -DCMAKE_CXX_COMPILER=g++-10
```

- Fedora:
  - `sudo dnf install autoconf ccache cmake fmt-devel gcc{,-c++} glslang hidapi-devel json-devel libtool libusb1-devel libzstd-devel lz4-devel nasm ninja-build openssl-devel pulseaudio-libs-devel python3-pip qt5-linguist qt5-qtbase{-private,}-devel qt5-qtwewbengine-devel speexdsp-devel wayland-devel zlib-devel ffmpeg-devel`
  - `pip install --user conan`
  - Fedora 32 or later is required.
  - Due to GCC 12, Fedora 36 or later users need to install `clang`, and configure CMake to use it via `-DCMAKE_CXX_COMPILER=clang++ -DCMAKE_C_COMPILER=clang`
  - CMake arguments to force system libraries:
    - SDL2: `-DYUZU_USE_BUNDLED_SDL2=OFF -DYUZU_USE_EXTERNAL_SDL2=OFF`
    - FFmpeg: `-DYUZU_USE_EXTERNAL_FFMPEG=OFF`
  - [RPM Fusion](https://rpmfusion.org/) (free) is required to install `ffmpeg-devel`
- RHEL-like (such as Rocky Linux):
  - Though this should have been similar to Fedora, this ends up being a tad bit more involved due to the distro's older or missing packages. Fortunately, at least Rocky Linux 8 makes `g++-10` available directly in the package manager, so it's just a matter of finding the other smaller dependencies. (CentOS 8 does **not** have `g++-10`, so it is even less trivial to build yuzu there.)
  - `sudo dnf config-manager --set-enabled powertools # Required for ninja-build and nasm`
  - `sudo dnf install alsa-lib-devel gcc-toolset-10-gcc-g++ git libXext-devel libzip-devel libzip-tools libzstd-devel lz4-devel make ninja-build openssl-devel opus-devel pulseaudio-libs-devel python36 qt5-linguist qt5-qtbase-devel qt5-qtbase-private-devel zlib-devel`
  - `pip install --user conan`
  - Distro version 8 or later is required.
  - Additional notes:
    - `/opt/rh/gcc-toolset-10/root/usr/bin` must be added to the front of the `PATH`.
    - [CMake](https://cmake.org/download/) (cmake-[version]-linux-x86_64.tar.gz) and [glslangValidator](https://github.com/KhronosGroup/glslang/releases/latest) (glslang-master-linux-Release.zip) must be downloaded and installed separately. To "install" them, extract the archives and copy their contents into the `$HOME/.local/`, such that the directory structure looks like `$HOME/.local/bin` and so on. -->
- Gentoo:
  - **\*\*Disclaimer\*\***: this dependency list was written by a novice Gentoo user who first set it up with a DE, and then based this list off of the Fedora dependency list. This may be missing some requirements, or includes too many. Caveat emptor.
  - `emerge --ask app-arch/lz4 dev-libs/boost dev-libs/hidapi dev-libs/libzip dev-libs/openssl dev-python/pip dev-qt/linguist dev-qt/qtconcurrent dev-qt/qtcore dev-util/cmake dev-util/glslang dev-vcs/git media-libs/alsa-lib media-libs/opus media-sound/pulseaudio media-video/ffmpeg net-libs/mbedtls sys-libs/zlib x11-libs/libXext`
  - `pip install --user conan`
  - GCC 10 or later is required.
  - Users may need to append `pulseaudio`, `bindist` and `context` to the `USE` flag.

### If this is your first time installing Conan:

If this your first time installing Conan, **you may have to log in and log out again** if you are on a Ubuntu-based distribution (alternatively, you can ensure your `$PATH` has been updated).

This is because `$HOME/.local/bin` needs to be included in the `PATH` variable. Check your `$HOME/.profile` and `$HOME/.bashrc` files, if `PATH=$HOME/.local/bin:$PATH` is not present, append that line to one of either file, then log out and log back in. Fedora and Ubuntu by default already have this covered, though Ubuntu users should log out and log back in to enable it.

### Cloning yuzu with Git

**Master:**

  ```bash
  git clone --recursive https://github.com/yuzu-emu/yuzu
  cd yuzu
  ```

**Mainline:**

  ```bash
  git clone --recursive https://github.com/yuzu-emu/yuzu-mainline
  cd yuzu-mainline
  ```

The `--recursive` option automatically clones the required Git submodules.

### Building yuzu in Release Mode (Optimized)

```bash
mkdir build && cd build
cmake .. -GNinja
ninja
sudo ninja install # (currently doesn't work, needs to be fixed)
```

Optionally, you can use `cmake-gui ..` to adjust various options (e.g. disable the Qt GUI).

### Building yuzu in Debug Mode (Slow)

```bash
mkdir build && cd build
cmake .. -GNinja -DCMAKE_BUILD_TYPE=Debug
ninja
```

### Building with debug symbols

```bash
mkdir build && cd build
cmake .. -GNinja -DCMAKE_BUILD_TYPE=RelWithDebInfo
ninja
```

### Running without installing

After building, the binaries `yuzu` and `yuzu-cmd` (depending on your build options) will end up in `build/bin/`.

  ```bash
  # SDL
  cd build/bin/
  ./yuzu-cmd

  # Qt
  cd build/bin/
  ./yuzu
  ```

### Debugging

```bash
cd data
gdb ../build/bin/yuzu            # Start GDB
(gdb) handle SIGSEGV nostop      # Disable SIGSEGV exceptions, which are used by yuzu for memory access
(gdb) run                        # Run yuzu under GDB
<crash>
(gdb) bt                         # Print a backtrace of the entire callstack to see which codepath the crash occurred on
```