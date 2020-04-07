### **How do I get games?**
_You are legally required to dump your games from your Nintendo Switch. To do so, please follow our in-depth [Quickstart Guide](https://yuzu-emu.org/help/quickstart/)_

### **yuzu starts with the error "Missing Derivation Components"**
_Please follow our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/) to dump your keys and system files from your Nintendo Switch._

### **yuzu starts with the error “VCRUNTIME140_1.dll was not found”**
_Please download and install the following dependencies:_

_https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads_

_Install the x64 version._

### **yuzu starts with the error "Unable to start application: Os { code: 2, kind: NotFound, message: “The system cannot find the file specified.” }"**

_This problem is usually caused by a false positive of your virus scanner, most recently avast and awg._

_You can confirm it is a false positive with an online scanner such as VirusTotal if you wish._

_To fix this you'll need to either disable or uninstall your virus scanner. Make sure to reboot if you choose to uninstall it._

_Afterwards follow the instructions below for `yuzu won't update anymore` to delete any residual files of the failed installation._

### **yuzu won't update anymore / starts with a platform error**
* _Close all instances of yuzu or the installer/maintenance tool you may have running._
* _Open `%localappdata%` in your file browser._
* _Select the `yuzu` folder and delete it._
* _Run the installer again._

### **How do I use mods?**
_For a list of useful mods for your favorite games, check our database with [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/)_

_To add mods to a specific game, simply right click the game in yuzu's games list, select `Open Mod Data Location` and structure your mod files similar to this example:_

_`Mod directory/mod name/romfs`_
_or_
_`Mod directory/mod name/exefs`_

_The mods provided on our [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/) page are already structured accordingly and only need to be extracted into the mod directory folder as is._

_Once added to the correct mod directory, simply right click the game again, select properties and activate the installed mod. The same process can be followed in reverse for de-activating mods_

### **How do I uninstall game updates or DLC?**
_Due to current file system limitations, there is no easy way to uninstall a specific update/DLC._

_It is usually easiest to just delete everything and then reinstall any updates and DLC that you need._

_Installed updates/DLC are found in `%appdata%\yuzu\nand\user\Contents\registered\`._

_To remove them, you will need to delete this `registered` folder._

_Remember to reinstall any updates or DLC you need._

_Afterwards, go to `Settings > System > Filesystem tab` and click on `Reset Metadata Cache` on bottom. This will refresh the gameslist addons column._

### **How do I set up my controls?**
_Set controls to `Custom`, then click on `Configure`._

_**For all games other than Pokemon Let's Go set the controls like this:**_

![](https://cdn.discordapp.com/attachments/400106910231035904/690188034087714847/pro.png)

* _Map your controls by clicking on `Configure` next to `Pro Controller`._
* _Make sure to map your analog sticks by clicking on the `Set analog Stick` button if you are using a controller._
* _Restart yuzu after you are done for the new settings to take effect_

_**For Pokemon Let's Go set your controls like this:**_

![](https://cdn.discordapp.com/attachments/400106910231035904/689931041720238097/PLG.png)

* _Map your controls by clicking on `Configure` next to the `Joycons Docked` checkbox._
* _Make sure `Player 1` is set to `None` as depicted in the screenshot._
* _Make sure to map your analog sticks by clicking on the `Set analog Stick` button if you are using a controller._
* _Restart yuzu after you are done for the new settings to take effect_

---

### **What is yuzu?**
_yuzu is an experimental open-source emulator for the Nintendo Switch from the creators of Citra._
_It is written in C++ with portability in mind, with builds actively maintained for Windows, Linux and macOS. The emulator currently can play various commercial titles and homebrew applications with varying degrees of success._

### **Which software license is yuzu licensed under?**
_yuzu is an open-source project, licensed under the GPLv2 (or any later version). Refer to the license document for more information._

### **Which platforms does yuzu support?**
_yuzu is actively tested and supported on various 64-bit versions of Windows (7 and up) and Linux. macOS is no longer supported due to Apple deprecating OpenGL._

### **What are the system requirements for yuzu?**
_yuzu currently requires a OpenGL 4.5 capable GPU and a CPU that has high single core performance. It also requires a minimum of 8 GB of RAM._

### **How do I build yuzu for the OS that I use?**
_Take a look at the following guides for steps on building yuzu for the following platforms:_
  - _[Linux](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Linux)_
  - _[macOS](https://github.com/yuzu-emu/yuzu/wiki/Building-for-macOS)_
  - _[Windows](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Windows)_

### **Who made yuzu?**
_yuzu has an active team of open-source developers. The list of contributors can be [found on GitHub](https://github.com/yuzu-emu/yuzu/graphs/contributors)._