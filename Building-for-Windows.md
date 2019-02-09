## THIS GUIDE IS INTENDED FOR DEVELOPERS ONLY, SUPPORT WILL ONLY BE GIVEN IF YOU'RE A DEVELOPER.

## MSVC Build for Windows

### Minimal Dependencies

On Windows, all library dependencies are automatically included within the "externals" folder or can be downloaded on-demand. To build yuzu, you simply need to install:

* **[Visual Studio 2017 Community](https://www.visualstudio.com/products/visual-studio-community-vs)** - **Make sure to select C++ support in the installer**.
* **[CMake](http://www.cmake.org/cmake/resources/software.html)** - Used to generate Visual Studio project files.

![2](https://i.imgur.com/S1NH63P.png)

* **Git** - We recommend [msysgit](http://msysgit.github.io/).

![3](http://i.imgur.com/joCBhIB.jpg)

* While installing Git Bash, you should tell it to include Git in your system path. (Choose the "Use Git from the Windows Command Prompt" option.) If you missed that, don't worry, you'll just have to manually tell CMake where your git.exe is, since it's used to include version info into the built executable.

![4](http://i.imgur.com/th8sFud.jpg)

### Cloning yuzu with Git

**Nightly (master):**
```
cmd
git clone --recursive https://github.com/yuzu-emu/yuzu.git
cd yuzu
```

**Canary:**
```
cmd
git clone --recursive https://github.com/yuzu-emu/yuzu-canary.git
cd yuzu
```

![9](https://i.imgur.com/xq15xTB.png)

NOTE: yuzu by default downloads to `C:\Users\<user-name>\yuzu` (Nightly) or `C:\Users\<user-name>\yuzu-canary` (Canary)

### Building

* Open cmake-gui and point it to the yuzu directory.

![10](https://i.imgur.com/YKmNs1p.png)
![11](https://i.imgur.com/SWxOVKB.png)

* For the build directory, use a `build/` subdirectory inside the source directory or some other directory of your choice. (Tell CMake to create it.)

* Click the "Configure" button and choose "Visual Studio 15 2017 Win64"

![12](http://i.imgur.com/RvVcyCP.jpg)

* NOTE: If you used GitHub's own app to clone, run `git submodule update --init --recursive` to get the remaining dependencies.
* Click "Generate" to create the project files.

![15](http://i.imgur.com/CkZgD4p.jpg)

* Open the solution file yuzu.sln in Visual Studio 2017, which is located in the build folder.

![16](https://i.imgur.com/q4dSKXR.png)

* Depending if you want a graphical user interface or not ("yuzu" is with a graphical user interface, while "yuzu-cmd" is just the command line version of it), select "yuzu" or "yuzu-cmd" in the Solution Explorer, right-click and "Set as StartUp Project".

![17](https://i.imgur.com/2h8q6at.png)

![18](http://i.imgur.com/FkuAwd8.jpg)

* Select the appropriate build type, Debug for debug purposes or Release for performance (in case of doubt choose the latter).

![19](http://i.imgur.com/Gqifkc0.jpg)

* Press F5 or select Build → Rebuild Solution in the menu.

![20](http://i.imgur.com/7ro9uSB.jpg)

Feel free to ask us in the IRC channel #yuzu @ [Freenode](https://webchat.freenode.net/) or on [Discord](https://discord.gg/XQV6dn9) if you have issues.

## MinGW-w64 Build with MSYS2

### Prerequisites to install

* [MSYS2](http://msys2.github.io/)

Make sure to follow the instructions and update to the latest version by running `pacman -Syu` as many times as needed.

### Install yuzu dependencies for MinGW-w64

* Open the "MSYS2 MinGW 64-bit" (mingw64.exe) shell
* Download and install all dependencies using: `pacman -S mingw-w64-x86_64-toolchain mingw-w64-x86_64-qt5 mingw-w64-x86_64-SDL2 mingw-w64-x86_64-cmake make git python2`

### Clone the yuzu repository with Git

**Nightly (master):**
```
git clone --recursive https://github.com/yuzu-emu/yuzu.git
cd yuzu
```

**Canary:**
```
git clone --recursive https://github.com/yuzu-emu/yuzu-canary.git
cd yuzu-canary
```

### Run the following commands to build yuzu (dynamic linked build)

```cmd
mkdir build && cd build
cmake -G "MSYS Makefiles" -DCMAKE_MAKE_PROGRAM=mingw32-make -DCMAKE_BUILD_TYPE=Release ..
mingw32-make -j4
# test yuzu out with
./bin/yuzu.exe
```

**Note! This build is not a static build meaning that you need to include all of the dlls with the exe in order to use it.**

### Building without Qt (Optional)

Doesn't require the rather large Qt dependency, but you will lack a GUI frontend.

* Pass the `-DENABLE_QT=no` flag to cmake

## Building from the command line with MSVC

```
git clone --recursive https://github.com/yuzu-emu/yuzu
cd yuzu
mkdir build
cd build
cmake .. -G "Visual Studio 15 2017 Win64"
cmake --build .
```