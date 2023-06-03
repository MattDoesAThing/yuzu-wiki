## Note: These build instructions are a work-in-progress.
### Dependencies
* [Android Studio](https://developer.android.com/studio)
* [NDK and CMake](https://developer.android.com/studio/projects/install-ndk#default-version)
* [Git](https://git-scm.com/download)
### Cloning yuzu with Git
```
git clone --recursive https://github.com/yuzu-emu/yuzu.git
```
Citra by default will be cloned into -
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

 