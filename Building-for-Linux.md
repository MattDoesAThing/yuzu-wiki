### Dependencies:

You'll need to download and install the following to build yuzu:

* [SDL2](https://www.libsdl.org/download-2.0.php)
  - Deb: `apt-get install sdl2` or `apt-get install libsdl2-2.0-0` or `apt-get install libsdl2-dev`
  - Arch: `pacman -S sdl2`
  - Fedora: `dnf install SDL2-devel`
* [Qt](http://qt-project.org/downloads)
  - Deb: `apt-get install qtbase5-dev libqt5opengl5-dev`
  - Arch: `pacman -S qt5`
  - Fedora: `dnf install qt5-qtbase qt5-qtbase-devel`
* GCC v5+ (for C++14 support)
  - Deb: `apt-get install build-essential`
  - Arch: `pacman -S base-devel`
  - Fedora: `dnf install gcc-c++`
* [CMake](http://www.cmake.org/) 3.6+
  - Deb: `apt-get install cmake`
  - Arch: `pacman -S cmake`
  - Fedora: `dnf install cmake`
* [Clang](https://github.com/llvm-mirror/clang) 3.8 (optional build alternative)
  - Deb: `apt-get install clang libc++-dev` (in some distros, clang-3.8).
  - Arch: `pacman -S clang`, `libc++` is in the AUR. Use pacaur or yaourt to install it.
* Curl
  - Deb: `apt-get install libcurl4-openssl-dev`
  - Arch `pacman -S libcurl-compat`

### Cloning yuzu in Git:

```
git clone --recursive https://github.com/yuzu-emu/yuzu
cd yuzu
```

The `--recursive` option automatically clones the required Git submodules too.

### Building unicorn:

```
cd externals
git clone https://github.com/yuzu-emu/unicorn
cd unicorn
UNICORN_ARCHS=aarch64 ./make.sh
export UNICORNDIR=$(pwd)
cd ../..
```

### Building yuzu in Debug Mode (Slow):

**Using gcc:**

```
mkdir build && cd build
cmake ../ -DUSE_SYSTEM_CURL=1
make
sudo make install
```
Optionally, you can use "cmake -i .." to adjust various options (e.g. disable the Qt GUI).

**Using clang:**

Note: It is important you use libc++ vs. , otherwise your build will likely fail. libc++ is not 100% complete on GNU/Linux, but works well for this build. The libstdc++ std::string is a different data structure than the libc++ std::string. See: [LLVLM.org](https://llvm.org/svn/llvm-project/www-releases/trunk/3.8.0/projects/libcxx/docs/UsingLibcxx.html). If libc++ is not used, some warnings are treated as errors. Using clang is only really recommended for users not using GCC >= 5. Also see [Clang Comparison](http://clang.llvm.org/comparison.html).

```
mkdir build && cd build
cmake  -DCMAKE_CXX_COMPILER=clang++-3.8 \
	-DCMAKE_C_COMPILER=clang-3.8 \
	-DCMAKE_CXX_FLAGS="-O2 -g -stdlib=libc++" \
        -DUSE_SYSTEM_CURL=1  ..
make
sudo make install (currently doesn't work, needs to be fixed)
```
Debian/Ubuntu: Owing to bug [#808086](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=808086) the build might
fail. To have it build, add the following after line 1938 of `/usr/include/c++/v1/string`. (see discussion on
[StackOverflow](http://stackoverflow.com/questions/37096062/get-a-basic-c-program-to-compile-using-clang-on-ubuntu-16)
for more details.)

```
#if _LIBCPP_STD_VER <= 14
    _NOEXCEPT_(is_nothrow_copy_constructible<allocator_type>::value)
#else
    _NOEXCEPT
#endif
```

Additionally, on Ubuntu,
do `sudo apt-get install libc++abi-dev && sudo ln -s /usr/include/libcxxabi/__cxxabi_config.h /usr/include/c++/v1/__cxxabi_config.h`


### Building yuzu in Release Mode (Optimized):

```
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DUSE_SYSTEM_CURL=1
make
sudo make install (currently doesn't work, needs to be fixed)
```

### Building with debug symbols:

```
cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo -DUSE_SYSTEM_CURL=1
make
```

### Running without installing:

After building, the binaries `yuzu` and `yuzu-qt` (depending on your build options) will end up in `build/src/<binary_name>/`. 

```
# SDL
cd build/src/yuzu/
./yuzu

# Qt
cd build/src/yuzu_qt/
./yuzu-qt
```

### Debugging:

```
cd data
gdb ../build/src/yuzu_qt/yuzu-qt
(gdb) run
<crash>
(gdb) bt
```