This article was written for developers. yuzu support for macOS is not ready for casual use.
---

Install dependencies from Homebrew:
```sh
brew install autoconf automake boost@1.76 ccache ffmpeg fmt glslang hidapi libtool libusb lz4 ninja nlohmann-json openssl qt@5 sdl2 speexdsp zlib zlib zstd
```

Build with debug symbols (vcpkg is not currently used due to broken boost-context library):
```sh
mkdir build && cd build
cmake .. -GNinja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DYUZU_USE_BUNDLED_VCPKG=OFF -DYUZU_TESTS=OFF
ninja
```

Run the output:
```
bin/yuzu.app/Contents/MacOS/yuzu
```