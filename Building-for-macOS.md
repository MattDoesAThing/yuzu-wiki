Please note this article is intended for development, and yuzu on macOS is not currently ready for regular use.

This article was written for developers. yuzu support for macOS is not ready for casual use.
---

Install dependencies from Homebrew:
```sh
brew install autoconf automake boost@1.76 ccache ffmpeg fmt glslang hidapi libtool libusb lz4 ninja nlohmann-json openssl qt@5 sdl2 speexdsp zlib zlib zstd
```

Build with debug symbols (vcpkg is not currently used due to broken boost-context library):
```sh
mkdir build && cd build
export Qt5_DIR="/opt/homebrew/opt/qt@5/lib/cmake"
cmake .. -GNinja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DYUZU_USE_BUNDLED_VCPKG=OFF -DYUZU_TESTS=OFF -DENABLE_WEB_SERVICE=OFF
ninja
```

Run the output:
```
bin/yuzu.app/Contents/MacOS/yuzu
```

---

To run with MoltenVK, install additional dependencies:
```sh
brew install molten-vk vulkan-loader
```

Run with Vulkan loader path:
```sh
export LIBVULKAN_PATH=/opt/homebrew/lib/libvulkan.dylib
bin/yuzu.app/Contents/MacOS/yuzu
```