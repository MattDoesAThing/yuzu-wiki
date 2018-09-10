### Dependencies

You'll need to download and install the following to build yuzu:

- [SDL2](https://www.libsdl.org/download-2.0.php)
  - Arch: `pacman -S sdl2`
  - Debian: `apt-get install sdl2` or `apt-get install libsdl2-2.0-0` or `apt-get install libsdl2-dev`
  - Fedora: `dnf install SDL2-devel`
  - Gentoo: `emerge media-libs/libsdl2`
- [Qt](http://qt-project.org/downloads)
  - Arch: `pacman -S qt5`
  - Debian: `apt-get install qtbase5-dev libqt5opengl5-dev`
  - Fedora: `dnf install qt5-qtbase qt5-qtbase-devel`
  - Gentoo: `emerge dev-qt/qtcore dev-qt/qtopengl`
- GCC v7+ (for C++17 support)
  - Arch: `pacman -S base-devel`
  - Debian: `apt-get install build-essential`
  - Fedora: `dnf install gcc`
  - Gentoo: `emerge =sys-devel/gcc-7.1.0`
- [CMake](http://www.cmake.org/) 3.6+
  - Arch: `pacman -S cmake`
  - Debian: `apt-get install cmake`
  - Fedora: `dnf install cmake`
  - Gentoo: `emerge dev-util/cmake`

Note: Depending on your distro, the version of CMake you get may not be what's required to build yuzu. Check with cmake --version. Version 3.6 or greater is required for you to be able to build!

- [Clang](https://github.com/llvm-mirror/clang) 3.8 (optional build alternative)
  - Arch: `pacman -S clang`, `libc++` is in the AUR. Use yay to install it.
  - Debian: `apt-get install clang libc++-dev` (in some distros, clang-3.8).
  - Gentoo: `emerge sys-devel/clang sys-libs/libcxx`

### Cloning yuzu with Git

```bash
git clone --recursive https://github.com/yuzu-emu/yuzu
cd yuzu
```

The `--recursive` option automatically clones the required Git submodules too.

### Building yuzu in Debug Mode (Slow)

#### Using GCC

```bash
mkdir build && cd build
cmake ../
make
sudo make install
```

Optionally, you can use `cmake -i ..` to adjust various options (e.g. disable the Qt GUI).

#### Using clang

Note: It is important you use libc++ vs. , otherwise your build will likely fail. libc++ is not 100% complete on GNU/Linux, but works well for this build. The libstdc++ std::string is a different data structure than the libc++ std::string. See: [LLVLM.org](https://llvm.org/svn/llvm-project/www-releases/trunk/3.8.0/projects/libcxx/docs/UsingLibcxx.html). If libc++ is not used, some warnings are treated as errors. Using clang is only really recommended for users not using GCC >= 5. Also see [Clang Comparison](http://clang.llvm.org/comparison.html).

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
[StackOverflow](http://stackoverflow.com/questions/37096062/get-a-basic-c-program-to-compile-using-clang-on-ubuntu-16)
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