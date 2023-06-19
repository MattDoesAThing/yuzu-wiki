# THIS GUIDE IS INTENDED FOR DEVELOPERS ONLY, SUPPORT WILL ONLY BE GIVEN IF YOU'RE A DEVELOPER.

## Method I: MSVC Build for Windows

### Minimal Dependencies

On Windows, all library dependencies are automatically included within the `externals` folder, or can be downloaded on-demand. To build yuzu, you need to install:

  * **[Visual Studio 2022 Community](https://visualstudio.microsoft.com/downloads/)** - **Make sure to select C++ support in the installer. Make sure to update to the latest version if already installed.**
  * **[CMake](https://cmake.org/download/)** - Used to generate Visual Studio project files. Does not matter if either 32-bit or 64-bit version is installed.
  * **[Vulkan SDK](https://vulkan.lunarg.com/sdk/home#windows)** - **Make sure to select Latest SDK.**

  ![2](https://i.imgur.com/giDwuTm.png)

  * **Git** - We recommend [Git for Windows](https://gitforwindows.org).

  ![3](https://i.imgur.com/UeSzkBw.png)

  * While installing Git Bash, you should tell it to include Git in your system path. (Choose the "Git from the command line and also from 3rd-party software" option.) If you missed that, don't worry, you'll just have to manually tell CMake where your git.exe is, since it's used to include version info into the built executable.

  ![4](https://i.imgur.com/x0rRs1t.png)

### Cloning yuzu with Git

**Master:**
  ```cmd
  git clone --recursive https://github.com/yuzu-emu/yuzu.git
  cd yuzu
  ```

**Mainline (no assert):**
  ```cmd
  git clone --recursive https://github.com/yuzu-emu/yuzu-mainline.git
  cd yuzu-mainline
  ```

  ![9](https://i.imgur.com/CcxIAht.png)

* *(Note: yuzu by default downloads to `C:\Users\<user-name>\yuzu` (Master) or `C:\Users\<user-name>\yuzu-mainline` (Mainline)*

### Building

* Open the CMake GUI application and point it to the `yuzu` (Master) or `yuzu-mainline` (Mainline) directory.

  ![10](https://i.imgur.com/qOslIWv.png)

* For the build directory, use a `/build` subdirectory inside the source directory or some other directory of your choice. (Tell CMake to create it.)

  ![11](https://i.imgur.com/cNnhs22.png)

* Click the "Configure" button and choose `Visual Studio 17 2022`, with `x64` for the optional platform.

  ![12](https://i.imgur.com/DKiREaK.png)

  * *(Note: If you used GitHub's own app to clone, run `git submodule update --init --recursive` to get the remaining dependencies)*

* If you get an error about missing packages, enable `YUZU_USE_BUNDLED_VCPKG`, and then click Configure again.

  * *(You may also want to disable `YUZU_TESTS` in this case since Catch2 is not yet supported with this.)*

  ![13](https://user-images.githubusercontent.com/22451773/180585999-07316d6e-9751-4d11-b957-1cf57cd7cd58.png)

* Click "Generate" to create the project files.

  ![15](https://i.imgur.com/5LKg92k.png)

* Open the solution file `yuzu.sln` in Visual Studio 2022, which is located in the build folder.

  ![16](https://i.imgur.com/208yMml.png)

* Depending if you want a graphical user interface or not (`yuzu` has the graphical user interface, while `yuzu-cmd` doesn't), select `yuzu` or `yuzu-cmd` in the Solution Explorer, right-click and `Set as StartUp Project`.

  ![17](https://i.imgur.com/nPMajnn.png)  ![18](https://i.imgur.com/BDMLzRZ.png)

* Select the appropriate build type, Debug for debug purposes or Release for performance (in case of doubt choose Release).

  ![19](https://i.imgur.com/qxg4roC.png)

* Right-click the project you want to build and press Build in the submenu or press F5.

  ![20](https://i.imgur.com/CkQgOFW.png)

Feel free to ask us in the IRC channel #yuzu-emu @ [libera](https://web.libera.chat) or on [Discord](https://discord.com/invite/u77vRWY) if you have issues.

## Method II: MinGW-w64 Build with MSYS2

### Prerequisites to install

* [MSYS2](https://www.msys2.org)
* [Vulkan SDK](https://vulkan.lunarg.com/sdk/home#windows) - **Make sure to select Latest SDK.**
* Make sure to follow the instructions and update to the latest version by running `pacman -Syu` as many times as needed.

### Install yuzu dependencies for MinGW-w64

* Open the `MSYS2 MinGW 64-bit` (mingw64.exe) shell
* Download and install all dependencies using: `pacman -Syu git make mingw-w64-x86_64-SDL2 mingw-w64-x86_64-cmake mingw-w64-x86_64-python-pip mingw-w64-x86_64-qt5 mingw-w64-x86_64-toolchain autoconf libtool automake-wrapper`
* Add MinGW binaries to the PATH: `echo 'PATH=/mingw64/bin:$PATH' >> ~/.bashrc`
* Add glslangValidator to the PATH: `echo 'PATH=$(readlink -e /c/VulkanSDK/*/Bin/):$PATH' >> ~/.bashrc`

### Clone the yuzu repository with Git

  ```bash
  git clone --recursive https://github.com/yuzu-emu/yuzu.git
  cd yuzu
  ```

### Run the following commands to build yuzu (dynamically linked build)

```bash
mkdir build && cd build
cmake -G "MSYS Makefiles" -DYUZU_USE_BUNDLED_VCPKG=ON -DYUZU_TESTS=OFF ..
make -j$(nproc)
# test yuzu out with
./bin/yuzu.exe
```

* *(Note: This build is not a static build meaning that you need to include all of the DLLs with the .exe in order to use it!)*

e.g.
```Bash
cp externals/ffmpeg-*/bin/*.dll bin/
```

Bonus Note: Running programs from inside `MSYS2 MinGW x64` shell has a different %PATH% than directly from explorer. This different %PATH% has the locations of the other DLLs required.
![image](https://user-images.githubusercontent.com/190571/165000848-005e8428-8a82-41b1-bb4d-4ce7797cdac8.png)


### Building without Qt (Optional)

Doesn't require the rather large Qt dependency, but you will lack a GUI frontend:

  * Pass the `-DENABLE_QT=no` flag to cmake

## Method III: CLion Environment Setup

### Minimal Dependencies

To build yuzu, you need to install the following:

* [CLion](https://www.jetbrains.com/clion/) - This IDE is not free; for a free alternative, check Method I
* [Vulkan SDK](https://vulkan.lunarg.com/sdk/home#windows) - Make sure to select the Latest SDK.

### Cloning yuzu with CLion

* Clone the Repository:

![1](https://user-images.githubusercontent.com/42481638/216899046-0d41d7d6-8e4d-4ed2-9587-b57088af5214.png)
![2](https://user-images.githubusercontent.com/42481638/216899061-b2ea274a-e88c-40ae-bf0b-4450b46e9fea.png)
![3](https://user-images.githubusercontent.com/42481638/216899076-0e5988c4-d431-4284-a5ff-9ecff973db76.png)



### Building & Setup

* Once Cloned, You will be taken to a prompt like the image below:

![4](https://user-images.githubusercontent.com/42481638/216899092-3fe4cec6-a540-44e3-9e1e-3de9c2fffc2f.png)

* Set the settings to the image below:
* Change `Build type: Release`
* Change `Name: Release`
* Change `Toolchain Visual Studio`
* Change `Generator: Let CMake decide`
* Change `Build directory: build`

![5](https://user-images.githubusercontent.com/42481638/216899164-6cee8482-3d59-428f-b1bc-e6dc793c9b20.png)

* Click OK; now Clion will build a directory and index your code to allow for IntelliSense. Please be patient.
* Once this process has been completed (No loading bar bottom right), you can now build yuzu
* In the top right, click on the drop-down menu, select all configurations, then select yuzu

![6](https://user-images.githubusercontent.com/42481638/216899226-975048e9-bc6d-4ec1-bc2d-bd8a1e15ed04.png)

* Now run by clicking the play button or pressing Shift+F10, and yuzu will auto-launch once built.

![7](https://user-images.githubusercontent.com/42481638/216899275-d514ec6a-e563-470e-81e2-3e04f0429b68.png)

## Building from the command line with MSVC

```cmd
git clone --recursive https://github.com/yuzu-emu/yuzu
cd yuzu
mkdir build
cd build
cmake .. -G "Visual Studio 17 2022" -A x64
cmake --build . --config Release
```