### Dependencies:

It's recommended that you use [homebrew](http://brew.sh/) to install dependencies.
You'll need to download and install the following to build yuzu:

* [pkg-config](https://www.freedesktop.org/wiki/Software/pkg-config/) (`brew install pkgconfig`)
* [SDL2](https://www.libsdl.org/download-2.0.php) (`brew install sdl2`)
* [Qt5](https://www.qt.io/download/) (`brew install qt5`) (**Note:** If you have Qt4 installed, then you will need to remove it before building. `brew unlink qt4`)
* [CMake](https://cmake.org/) (`brew install cmake`)
* A recent version of Xcode and the Xcode command line tools

### Cloning yuzu in Git:

```
git clone --recursive https://github.com/yuzu-emu/yuzu
cd yuzu
git submodule update --init --recursive
```

### Building unicorn:

```
pushd externals
git clone https://github.com/yuzu-emu/unicorn
cd unicorn
UNICORN_ARCHS=aarch64 ./make.sh macos-universal-no
export UNICORNDIR=$(pwd)
popd
```

### Using CMake:

First of all, you have to tell CMake where your Qt5 is installed (add this line to ~/.profile if you want to make this permanent.):

```
export Qt5_DIR=$(brew --prefix)/opt/qt5
```

Now you can generate makefiles for the build:
```
export MACOSX_DEPLOYMENT_TARGET=10.9
mkdir build
cd build
cmake .. -DUSE_SYSTEM_CURL=ON -DCMAKE_OSX_ARCHITECTURES="x86_64;x86_64h" -DCMAKE_BUILD_TYPE=Release
```

This builds a fat binary that has slices targeting early and late x64 machines.

### Building yuzu

```
make -j4
```

Temporary unicorn fixup:

```
# copy libunicorn.1.dylib into yuzu.app/Contents/MacOS 
# then run:
install_name_tool -change libunicorn.1.dylib @executable_path/libunicorn.1.dylib yuzu.app/Contents/MacOS/yuzu
```

A `yuzu_qt.app` application bundle will now be present under `build/src/yuzu_qt/`. Note that this is non-portable and only works on your machine.

For portability of the appbundle between machines please refer to [this script](https://github.com/yuzu-emu/yuzu/blob/master/.travis/macos/upload.sh).