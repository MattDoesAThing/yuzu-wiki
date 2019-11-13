**Note: Mac OS is no longer supported due to Apple deprecating OpenGL and their current version not supporting the OpenGL extensions we require.**

### Dependencies

It's recommended that you use [Homebrew](http://brew.sh/) to install dependencies.
You'll need to download and install the following to build yuzu:

* [pkg-config](https://www.freedesktop.org/wiki/Software/pkg-config/) (`brew install pkgconfig`)
* [SDL2](https://www.libsdl.org/download-2.0.php) (`brew install sdl2`)
* [Qt5](https://www.qt.io/download/) (`brew install qt5`) (**Note:** If you have Qt4 installed, then you will need to remove it before building. `brew unlink qt4`)
* [CMake](https://cmake.org/) (`brew install cmake`)
* A recent version of Xcode and the Xcode command line tools

### Cloning yuzu with Git

**Master:**
```bash
git clone --recursive https://github.com/yuzu-emu/yuzu
cd yuzu
git submodule update --init --recursive
```

**Mainline (no assert):**
```bash
git clone --recursive https://github.com/yuzu-emu/yuzu-mainline
cd yuzu-mainline
git submodule update --init --recursive
```

### Using CMake

First of all, you have to tell CMake where Qt5 is installed (add this line to ~/.profile if you want to make this permanent):

```bash
export Qt5_DIR=$(brew --prefix)/opt/qt5
```

Now you can generate makefiles for the build:

```bash
export MACOSX_DEPLOYMENT_TARGET=10.14
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
```

### Building yuzu

```bash
make -j4
```

A `yuzu_qt.app` application bundle will now be present under `build/bin/`. Note that this is non-portable and only works on your machine.

For portability of the appbundle between machines please refer to [this script](https://github.com/yuzu-emu/yuzu/blob/master/.travis/macos/upload.sh).