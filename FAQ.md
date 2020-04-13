### **How do I get Games?**

_You are legally required to dump your games from your Nintendo Switch. To do so, please follow our in-depth [Quickstart Guide](https://yuzu-emu.org/help/quickstart/)._


### **yuzu starts with the error "Missing Derivation Components"**
![](https://cdn.discordapp.com/attachments/512678820092968971/699337208443699307/Keys_missing.PNG)

_yuzu requires console keys to play your games. Please follow our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/) to dump these keys and system files from your Nintendo Switch._

_These console keys (prod.keys/title.keys) need to be placed in the following directories_

* Windows: C:\Users\USERNAME\AppData\Roaming\yuzu\keys  **<- You need to make this "keys" folder**

* Linux: /home/USER/.local/share/yuzu/keys **<- You need to make this "keys" folder**

**NOTE: This yuzu directory can be quickly accessed by selecting file/open yuzu folder within the emulator**


### **yuzu starts with the error “VCRUNTIME140_1.dll was not found”**

![](https://cdn.discordapp.com/attachments/512678820092968971/699336946698158120/VC_missing.png)

_Current versions of yuzu require the latest versions of Microsoft Visual C++. Please download and install the following dependency:_

_https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads_

_Go to Visual Studio 2015, 2017 and 2019, and select the link next to x64._

### **yuzu starts with the error "Unable to start application: Os { code: 2, kind: NotFound, message: “The system cannot find the file specified.” }"**

_This problem is usually caused by a false positive of your antivirus software, most commonly by Avast and AVG. These applications will often incorrectly detect yuzu as malicious software and delete the executable as a result._

_You can confirm it is a false positive with an online scanner, such as [VirusTotal](https://www.virustotal.com) if you wish._

_To fix this, you'll need to either disable or uninstall your antivirus software. Make sure to reboot if you choose to uninstall it._

_Afterwards, follow the instructions below for `yuzu will not update further or starts with a Qt platform error` to delete any residual files of the failed installation._

### **yuzu will not update further or starts with a Qt platform error**
* _Close all instances of yuzu and any installer processes you may have running._
* _Press Win+R, in the opened window type `%localappdata%` and press Enter._
* _Select the `yuzu` folder and delete it. If it is being used by another process, please double-check that you do not have any yuzu related applications running._
* _Launch the installer and install yuzu again._

### **My game is Lagging and Dropping to Low Framerates**

_You are likely experiencing Shader Caching. Shaders are small programs running on a graphic card, responsible for rendering graphics like terrain, explosions, characters, etc. Since a PC cannot directly execute switch shaders, It first has to translate them to a format a PC can understand. This translation process is time-consuming and you'll notice it in two ways:_

* _While playing, if yuzu needs to translate a new shader, the game will stutter. Loading into a game for the first time can give long freezes due to the number of shaders. As you keep playing, the amount of stuttering will decrease._

* _When launching a game, the shader cache is loaded. To speed up this process there exists an additional "precompiled" cache. This cache may get reset every time you update yuzu or install a new GPU driver. The precompiled cache will then be compiled from scratch, causing a longer load time._

_Currently, the Vulkan renderer does not have a disk shader cache. This means that subsequent game loads will require the building of shaders each time._

`IMPORTANT: Since the cache stores parts of the game, we don't condone sharing or downloading these, since it is considered piracy`

### **How do I use mods?**
_For a list of useful mods for your favorite games, check our database with [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/)_

_To add mods to a specific game, simply right click the game in yuzu's games list, select `Open Mod Data Location` and structure your mod files similar to this example:_

_`Mod directory/mod name/romfs`_
_or_
_`Mod directory/mod name/exefs`_

_An example of a correctly structured mod directory can be seen below_

![](https://cdn.discordapp.com/attachments/512678820092968971/697113928852963378/Mod_Format.PNG)

_The mods provided on our [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/) page are already structured accordingly and only need to be extracted into the mod directory folder as is._

_Once added to the correct mod directory, simply right click the game again, select properties and activate the installed mod. The same process can be followed in reverse for de-activating mods_

![](https://cdn.discordapp.com/attachments/512678820092968971/697124627520159804/Mods_on.PNG)

### **How do I install game updates or DLC?**
_Installing updates and DLC is simple. In the top left corner of the emulator window, select `File / Install Files to NAND`, then select the file you wish to install. Once installed, your files should load automatically and the installed update or DLC will be shown in the games list add-ons column of the corresponding game._

_If you wish to activate/deactivate a specific update or DLC then right click your game in the games list, select `Properties`, then enable or disable as needed._

![](https://cdn.discordapp.com/attachments/512678820092968971/697129823407177789/Updates_and_DLC.PNG)

### **How do I uninstall game updates or DLC?**

_Due to current file system limitations, there is no easy way to uninstall a specific update/DLC._

_It is usually easiest to just delete everything and then reinstall any updates and DLC that you need._

_Installed updates/DLC are found in `%appdata%\yuzu\nand\user\Contents\registered\`._

_To remove them, you will need to delete this `registered` folder._

_Remember to reinstall any updates or DLC you need._

_Afterwards, go to `Settings / System / Filesystem tab` and click on `Reset Metadata Cache` on the bottom. This will refresh the games list addons column._

### **How do I set up my controls?**

_Since the Nintendo Switch is a complicated device controller input wise, you will need to change some input settings depending on the game you wish to play._

_In the input window dropdown, Select `Custom`, then click on `Configure`._

![](https://cdn.discordapp.com/attachments/356187763139280896/697133498074660904/Custom.PNG)

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

### **How do I add a save to my Game**

_To add a save, simply right-click your game in the Games List, Select `Open Save Data Location`, then Select your User from the Profile Selector_

![](https://cdn.discordapp.com/attachments/356187763139280896/697140759454941245/User_list_saves.PNG)

_Once your `Save Data Location` is open, place your game saves in this directory_

![](https://cdn.discordapp.com/attachments/356187763139280896/697142111568527400/save_location.PNG)
 
---

### **What is yuzu?**
_yuzu is an experimental open-source emulator for the Nintendo Switch from the creators of Citra._
_It is written in C++ with portability in mind, with builds actively maintained for Windows, Linux and macOS. The emulator currently can play various commercial titles and homebrew applications with varying degrees of success._

### **Which software license is yuzu licensed under?**
_yuzu is an open-source project, licensed under the GPLv2 (or any later version). Refer to the license document for more information._

### **Which platforms does yuzu support?**
_yuzu is actively tested and supported on various 64-bit versions of Windows (7 and up) and Linux. macOS is no longer supported due to Apple deprecating OpenGL._

### **What are the system requirements for yuzu?**
_yuzu currently requires an OpenGL 4.5 capable GPU and a CPU that has high single-core performance. It also requires a minimum of 8 GB of RAM. For more details, see our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/#hardware)._

### **How do I build yuzu for the OS that I use?**
_Take a look at the following guides for steps on building yuzu for the following platforms:_
  - _[Linux](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Linux)_
  - _[macOS](https://github.com/yuzu-emu/yuzu/wiki/Building-for-macOS)_
  - _[Windows](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Windows)_

### **Who made yuzu?**
_yuzu has an active team of open-source developers. The list of contributors can be [found on GitHub](https://github.com/yuzu-emu/yuzu/graphs/contributors)._