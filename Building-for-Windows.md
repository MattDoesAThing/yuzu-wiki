## THIS GUIDE IS INTENDED FOR DEVELOPERS ONLY, SUPPORT WILL ONLY BE GIVEN IF YOU'RE A DEVELOPER.

## Method I: MSVC Build for Windows

### Minimal Dependencies

On Windows, all library dependencies are automatically included within the "externals" folder or can be downloaded on-demand. To build yuzu, you simply need to install:

* **[Visual Studio 2017 Community](https://visualstudio.microsoft.com/downloads/)** - **Make sure to select C++ support in the installer. Visual Studio 2019 is not yet supported.**
* **[CMake](https://cmake.org/download/)** - Used to generate Visual Studio project files. Does not matter if either 32-bit or 64-bit version is installed.

![2](https://i.imgur.com/giDwuTm.png)

* **Git** - We recommend [Git for Windows](https://gitforwindows.org/).

![3](https://i.imgur.com/UeSzkBw.png)

* While installing Git Bash, you should tell it to include Git in your system path. (Choose the "Git from the command line and also from 3rd-party software" option.) If you missed that, don't worry, you'll just have to manually tell CMake where your git.exe is, since it's used to include version info into the built executable.

![4](https://i.imgur.com/x0rRs1t.png)

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
cd yuzu-canary
```

![9](https://i.imgur.com/CcxIAht.png)

* *(Note: yuzu by default downloads to `C:\Users\<user-name>\yuzu` (Nightly) or `C:\Users\<user-name>\yuzu-canary` (Canary)*

### Building

* Open the CMake GUI application and point it to the `yuzu` (Nightly) or `yuzu-canary` (Canary) directory.

![10](https://i.imgur.com/qOslIWv.png)

* For the build directory, use a `/build` subdirectory inside the source directory or some other directory of your choice. (Tell CMake to create it.)

![11](https://i.imgur.com/cNnhs22.png)

* Click the "Configure" button and choose "Visual Studio 15 2017", with "x64" for the optional platform.
* *(Note: older CMake versions prior to 3.14 combines these two options as "Visual Studio 15 2017 Win64")*

![12](https://i.imgur.com/p9kJ6EB.png)

* *(Note: If you used GitHub's own app to clone, run `git submodule update --init --recursive` to get the remaining dependencies)*
* Click "Generate" to create the project files.

![15](https://i.imgur.com/5LKg92k.png)

* Open the solution file yuzu.sln in Visual Studio 2017, which is located in the build folder.

![16](https://i.imgur.com/208yMml.png)

* Depending if you want a graphical user interface or not ("yuzu" is with a graphical user interface, while "yuzu-cmd" is just the command line version of it), select "yuzu" or "yuzu-cmd" in the Solution Explorer, right-click and "Set as StartUp Project".

![17](https://i.imgur.com/nPMajnn.png)  ![18](https://i.imgur.com/BDMLzRZ.png)

* Select the appropriate build type, Debug for debug purposes or Release for performance (in case of doubt choose Release).

![19](https://i.imgur.com/qxg4roC.png)

* Right-click the project you want to build and press Build in the submenu or press F5.

![20](https://i.imgur.com/CkQgOFW.png)

Feel free to ask us in the IRC channel #yuzu-emu @ [Freenode](https://webchat.freenode.net/) or on [Discord](https://discord.gg/XQV6dn9) if you have issues.

## Method II: MinGW-w64 Build with MSYS2

### Prerequisites to install

* [MSYS2](http://www.msys2.org/)

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

### Run the following commands to build yuzu (dynamically linked build)

```cmd
mkdir build && cd build
cmake -G "MSYS Makefiles" -DCMAKE_MAKE_PROGRAM=mingw32-make -DCMAKE_BUILD_TYPE=Release ..
mingw32-make -j4
# test yuzu out with
./bin/yuzu.exe
```

* *(Note: This build is not a static build meaning that you need to include all of the DLLs with the .exe in order to use it!)*

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