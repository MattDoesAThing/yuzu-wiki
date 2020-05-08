### Dependencies

You'll need to download and install the following to build yuzu:

  * GCC v7+ (for C++17 support) & misc
  * [CMake](https://www.cmake.org/) 3.6+
  * [SDL2](https://www.libsdl.org/download-2.0.php)
  * [Qt](https://qt-project.org/downloads)
  * [Python2](https://www.python.org/download/releases/2.7/) 2.7

All other dependencies will be downloaded by [conan](https://conan.io/downloads.html) if needed:

  * [Boost](https://www.boost.org/users/download/)
  * [Catch2](https://github.com/catchorg/Catch2)
  * [fmt](https://fmt.dev/)
  * [OpenSSL](https://www.openssl.org/source/)
  * [lz4](http://www.lz4.org)
  * [nlohmann_json](https://github.com/nlohmann/json)
  * [opus](https://opus-codec.org/downloads/)
  * [ZLIB](https://www.zlib.net/)
  * [zstd](https://facebook.github.io/zstd/)

      | Distro          | Commands
      | --------------- | ----------------
      | Arch            | `sudo pacman -S base-devel cmake sdl2 qt5 python2 python-pip boost catch2 fmt openssl lz4 mbedtls nlohmann-json opus zlib zip zstd && sudo pip install conan`
      | Ubuntu / Debian | `sudo apt-get install build-essential cmake libboost-all-dev libsdl2-2.0-0 libsdl2-dev qtbase5-dev libqt5opengl5-dev qtbase5-private-dev python2 python-pip && sudo pip install conan`
      | Fedora          | `sudo dnf install gcc cmake SDL2-devel qt5-qtbase qt5-qtbase-devel python2 python-pip && sudo pip install conan`
      | Gentoo          | `emerge =sys-devel/gcc-7.1.0 dev-util/cmake media-libs/libsdl2 dev-qt/qtcore dev-qt/qtopengl && sudo pip install conan`

Note: Depending on your distro, the version of CMake you get may not be what's required to build yuzu. Check with `cmake --version`. Version 3.6 or greater is required for you to be able to build!

  * [Clang](https://github.com/llvm-mirror/clang) 3.8 (optional build alternative):
      | Distro | Commands
      | ------ | ------------------
      | Arch   | `sudo pacman -S clang`, `libc++` is in the AUR. Use `yay` to install it.
      | Debian | `sudo apt-get install clang libc++-dev` (in some distros, clang-3.8)
      | Gentoo | `emerge sys-devel/clang sys-libs/libcxx`

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

### Building yuzu in Debug Mode (Slow)

#### Using GCC

```bash
mkdir build && cd build
cmake ../
make
sudo make install
```
Note: You can use **make -jN** where N is the number of processors available to accelerate building.

Optionally, you can use `cmake -i ..` to adjust various options (e.g. disable the Qt GUI).

#### Using clang

Note: It is important you use libc++ vs., otherwise your build will likely fail. libc++ is not 100% complete on GNU/Linux, but works well for this build. The libstdc++ std::string is a different data structure than the libc++ std::string. See: [LLVM.org](https://llvm.org/svn/llvm-project/www-releases/trunk/3.8.0/projects/libcxx/docs/UsingLibcxx.html). If libc++ is not used, some warnings are treated as errors. Using clang is only really recommended for users not using GCC >= 5. Also see [Clang Comparison](https://clang.llvm.org/comparison.html).

  ```bash
  mkdir build && cd build
  cmake -DCMAKE_CXX_COMPILER=clang++-3.8 \
        -DCMAKE_C_COMPILER=clang-3.8 \
        -DCMAKE_CXX_FLAGS="-O2 -g -stdlib=libc++" \
        ..
  make
  sudo make install # (currently doesn't work, needs to be fixed)
  ```

Debian/Ubuntu: Owing to bug [#808086](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=808086) the build might
fail. To have it build, add the following after line 1938 of `/usr/include/c++/v1/string`. (see discussion on
[StackOverflow](https://stackoverflow.com/questions/37096062/get-a-basic-c-program-to-compile-using-clang-on-ubuntu-16)
for more details.)

  ```cpp
  #if _LIBCPP_STD_VER <= 14
      _NOEXCEPT_(is_nothrow_copy_constructible<allocator_type>::value)
  #else
      _NOEXCEPT
  #endif
  ```

Additionally, on Ubuntu, do:

  ```bash
  sudo apt-get install libc++abi-dev && sudo ln -s /usr/include/libcxxabi/__cxxabi_config.h /usr/include/c++/v1/__cxxabi_config.h
  ```

### Building yuzu in Release Mode (Optimized)

```bash
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make
sudo make install # (currently doesn't work, needs to be fixed)
```

### Building with debug symbols

```bash
cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
make
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