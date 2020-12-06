**This article was written for developers. Users looking to simply run yuzu should try downloading [Mainline](https://yuzu-emu.org/downloads/) first. It requires installing the same dependencies listed below, though ` && pip install --user conan` can be omitted.**

### Dependencies

You'll need to download and install the following to build yuzu:

  * GCC v7+ (for C++17 support) & misc
  * [CMake](https://www.cmake.org/) 3.15+
  * [SDL2](https://www.libsdl.org/download-2.0.php)
  * [Qt](https://qt-project.org/downloads)
  * [Python2](https://www.python.org/download/releases/2.7/) 2.7
  * [FFmpeg](https://ffmpeg.org/)

All other dependencies will be downloaded by [conan](https://conan.io/downloads.html) if needed:

  * [Boost](https://www.boost.org/users/download/)
  * [Catch2](https://github.com/catchorg/Catch2)
  * [fmt](https://fmt.dev/)
  * [lz4](http://www.lz4.org)
  * [nlohmann_json](https://github.com/nlohmann/json)
  * [OpenSSL](https://www.openssl.org/source/)
  * [opus](https://opus-codec.org/downloads/)
  * [ZLIB](https://www.zlib.net/)
  * [zstd](https://facebook.github.io/zstd/)

      | Distro          | Commands
      | --------------- | ----------------
      | Arch            | `sudo pacman -S --needed git base-devel ninja cmake sdl2 qt5 python2 python-pip boost catch2 ffmpeg fmt libzip lz4 mbedtls nlohmann-json openssl opus zlib zstd && pip install --user conan`
      | Ubuntu / Mint | `sudo apt-get install git build-essential ninja-build cmake libsdl2-dev qtbase5-dev libqt5opengl5-dev qtwebengine5-dev qtbase5-private-dev python python3-pip libboost-dev libboost-context-dev libavcodec-dev libavutil-dev libswscale-dev libzip-dev liblz4-dev libmbedtls-dev libssl-dev libopus-dev zlib1g-dev libzstd-dev  && pip3 install --user conan`
      | Fedora          | `sudo dnf install git gcc ninja-build cmake make libzip-tools SDL2-devel qt5-qtbase-devel qt5-qtbase-private-devel qt5-qtwebengine-devel qt5-linguist python2 python-pip boost-devel fmt-devel libzip-devel libzstd-devel lz4-devel mbedtls-devel openssl-devel opus-devel zlib-devel ffmpeg-devel pulseaudio-libs-devel alsa-lib-devel jack-audio-connection-kit-devel && pip install --user conan`
      | Gentoo          | `emerge dev-vcs/git =sys-devel/gcc-7.1.0 dev-util/ninja dev-util/cmake media-libs/libsdl2 dev-qt/qtcore dev-qt/qtopengl && pip install --user conan`

After installing conan, `$HOME/.local/bin` needs to be included in the `PATH` variable. Check your `$HOME/.profile` and `$HOME/.bashrc` files, if `PATH=$HOME/.local/bin:$PATH` is not present, append that line to one of either file, then log out and log back in. Fedora and Ubuntu by default already have this covered.

Fedora users need to setup [RPM Fusion](https://rpmfusion.org/Configuration) (free) to install FFmpeg dependencies.

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