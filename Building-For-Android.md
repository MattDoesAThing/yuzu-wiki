## Note: These build instructions are a work-in-progress.
### Dependencies
* [Android Studio](https://developer.android.com/studio)
* [NDK 25.2.9519653 and CMake 3.22.1](https://developer.android.com/studio/projects/install-ndk#default-version)
* [Git](https://git-scm.com/download)
#### WINDOWS ONLY - Additional Dependencies
  * **[Visual Studio 2022 Community](https://visualstudio.microsoft.com/downloads/)** - **Make sure to select "Desktop development with C++" support in the installer. Make sure to update to the latest version if already installed.**
  * **[Vulkan SDK](https://vulkan.lunarg.com/sdk/home#windows)** - **Make sure to select Latest SDK.**
### Cloning yuzu with Git
```
git clone --recursive https://github.com/yuzu-emu/yuzu.git
```
yuzu by default will be cloned into -
* `C:\Users\<user-name>\yuzu` on Windows
* `~/yuzu` on Linux
* And wherever on macOS
### Building
1. Start Android Studio, on the startup dialog select `Open`.
2. Navigate to the `yuzu/src/android` directory and click on `OK`.
3. In `Build > Select Build Variant`, select `release` or `relWithDebInfo` as the "Active build variant".
4. Build the project with `Build > Make Project` or run it on an Android device with `Run > Run 'app'`.

### Additional Resources
https://developer.android.com/studio/intro

