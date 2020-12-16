> **This article was written for developers. Users looking to simply run yuzu should try downloading [Mainline](https://yuzu-emu.org/downloads/) first. It requires installing the same dependencies listed below, though `&& pip install --user conan` can be omitted.**

### Dependencies

You'll need to download and install the following to build yuzu:

  * GCC v10+ (for C++20 support) & misc
  * [CMake](https://www.cmake.org/) 3.15+
  * [SDL2](https://www.libsdl.org/download-2.0.php)
  * [Qt](https://qt-project.org/downloads)
  * [FFmpeg](https://ffmpeg.org/)

All other dependencies will be downloaded by [Conan](https://conan.io/downloads.html) if needed:

  * [Boost](https://www.boost.org/users/download/)
  * [Catch2](https://github.com/catchorg/Catch2)
  * [fmt](https://fmt.dev/)
  * [lz4](http://www.lz4.org)
  * [nlohmann_json](https://github.com/nlohmann/json)
  * [OpenSSL](https://www.openssl.org/source/)
  * [opus](https://opus-codec.org/downloads/)
  * [ZLIB](https://www.zlib.net/)
  * [zstd](https://facebook.github.io/zstd/)


- Arch / Manjaro:
  - `sudo pacman -Syu --needed base-devel boost catch2 cmake ffmpeg fmt git libzip lz4 mbedtls ninja nlohmann-json openssl opus python-pip python2 qt5 sdl2 zlib zstd && pip install --user conan`
  - GCC 10 or later is required.
- Ubuntu / Linux Mint / Debian:
  - `sudo apt-get install build-essential cmake g++-10 gcc-10 git libavcodec-dev libavutil-dev libboost-context-dev libboost-dev liblz4-dev libmbedtls-dev libopus-dev libqt5opengl5-dev libsdl2-dev libssl-dev libswscale-dev libzip-dev libzstd-dev ninja-build python python3-pip qtbase5-dev qtbase5-private-dev qtwebengine5-dev zlib1g-dev && pip3 install --user conan`
  - Ubuntu 20.04, Linux Mint 20, or Debian Bullseye or later is required.
  - Users need to manually specify building with GCC 10. This can be done by adding the parameters `-DCMAKE_C_COMPILER=gcc-10 -DCMAKE_CXX_COMPILER=g++-10` when running CMake. i.e.

```
cmake .. -GNinja -DCMAKE_C_COMPILER=gcc-10 -DCMAKE_CXX_COMPILER=g++-10
```
- Fedora:
  - `sudo dnf install SDL2-devel alsa-lib-devel boost-devel cmake ffmpeg-devel fmt-devel gcc git jack-audio-connection-kit-devel libzip-devel libzip-tools libzstd-devel lz4-devel make mbedtls-devel ninja-build openssl-devel opus-devel pulseaudio-libs-devel python-pip python2 qt5-linguist qt5-qtbase-devel qt5-qtbase-private-devel qt5-qtwebengine-devel zlib-devel && pip install --user conan`
  - Fedora 32 or later is required.
  - Users need to set up [RPM Fusion](https://rpmfusion.org/Configuration) (free) to install FFmpeg dependencies.
- Gentoo (this list needs updated with GCC 10, FFmpeg):
  - `emerge dev-vcs/git =sys-devel/gcc-7.1.0 dev-util/ninja dev-util/cmake media-libs/libsdl2 dev-qt/qtcore dev-qt/qtopengl && pip install --user conan`
  - GCC 10 or later is required.

After installing Conan, `$HOME/.local/bin` needs to be included in the `PATH` variable. Check your `$HOME/.profile` and `$HOME/.bashrc` files, if `PATH=$HOME/.local/bin:$PATH` is not present, append that line to one of either file, then log out and log back in. Fedora and Ubuntu by default already have this covered, though Ubuntu users should log out and log back in to enable it.


### Cloning yuzu with Git

**Master:**

  ```bash
  git clone --recursive https://github.com/yuzu-emu/yuzu
  cd yuzu
  ```

**Mainline (no assert):**

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
(gdb) run                        # Run yuzu under GDB
<crash>
(gdb) bt                         # Print a backtrace of the entire callstack to see which codepath the crash occurred on
```