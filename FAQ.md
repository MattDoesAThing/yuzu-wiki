If you are unable to find the answer to your question, please join our Discord server for support: [Discord Server](https://discord.gg/u77vRWY)

### **yuzu starts with the error “VCRUNTIME140_1.dll was not found”**

![](https://cdn.discordapp.com/attachments/512678820092968971/699336946698158120/VC_missing.png)

Current versions of yuzu require the latest versions of Microsoft Visual C++. Please download and install the following dependency:

https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads

Go to Visual Studio 2015, 2017 and 2019, and select the link next to x64.


### **How do I get Games?**

You are legally required to dump your games from your Nintendo Switch. To do so, please follow our in-depth [Quickstart Guide](https://yuzu-emu.org/help/quickstart/).


### **yuzu starts with the error "Missing Derivation Components"**
![](https://cdn.discordapp.com/attachments/512678820092968971/699337208443699307/Keys_missing.PNG)

yuzu requires console keys to play your games. Please follow our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/) to dump these keys and system files from your Nintendo Switch.

These console keys (prod.keys/title.keys) need to be placed in the following directories:

You may need to create the following "keys" folder:
* Windows: `C:\Users\USERNAME\AppData\Roaming\yuzu\keys`
* Linux: `/home/USERNAME/.local/share/yuzu/keys`

**NOTE: This yuzu directory can be quickly accessed by selecting file/open yuzu folder within the emulator**



### **yuzu starts with the error "Unable to start application: Os { code: 2, kind: NotFound, message: “The system cannot find the file specified.” }"**

This problem is usually caused by a false positive of your antivirus software, most commonly by Avast and AVG. These applications will often incorrectly detect yuzu as malicious software and delete the executable as a result.

You can confirm it is a false positive with an online scanner, such as [VirusTotal](https://www.virustotal.com) if you wish.

To fix this, you'll need to either disable or uninstall your antivirus software. Make sure to reboot if you choose to uninstall it.

Afterwards, follow the instructions below for `yuzu will not update further or starts with a Qt platform error` to delete any residual files of the failed installation.

### **yuzu will not update further or starts with a Qt platform error**

![](https://cdn.discordapp.com/attachments/356187763139280896/700495249817993266/QT_Error.PNG)

* Close all instances of yuzu and any installer processes you may have running.
* Press Win+R, in the opened window type `%localappdata%` and press Enter.
* Select the `yuzu` folder and delete it. If it is being used by another process, please double-check that you do not have any yuzu related applications running.
* Launch the installer and install yuzu again.

### **My game is Lagging and Dropping to Low Framerates**


You are likely experiencing Shader Caching. Shaders are small programs running on a graphic card, responsible for rendering graphics like terrain, explosions, characters, etc. Since a PC cannot directly execute switch shaders, It first has to translate them to a format a PC can understand. This translation process is time-consuming and you'll notice it in two ways:

* While playing, if yuzu needs to translate a new shader, the game will stutter. Loading into a game for the first time can give long freezes due to the number of shaders. As you keep playing, the amount of stuttering will decrease.

* When launching a game, the shader cache is loaded. To speed up this process there exists an additional "precompiled" cache. This cache may get reset every time you update yuzu or install a new GPU driver. The precompiled cache will then be compiled from scratch, causing a longer load time.

Currently, the Vulkan renderer does not have a disk shader cache. This means that subsequent game loads will require the building of shaders each time.

`IMPORTANT: Since the cache stores parts of the game, we don't condone sharing or downloading these, since it is considered piracy`

### **How do I use mods?**
For a list of useful mods for your favorite games, check our database with [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/)

To add mods to a specific game, simply right click the game in yuzu's games list, select `Open Mod Data Location` and structure your mod files similar to this example:

`Mod directory/mod name/romfs`
_or_
`Mod directory/mod name/exefs`

An example of a correctly structured mod directory can be seen below:

![](https://cdn.discordapp.com/attachments/512678820092968971/697113928852963378/Mod_Format.PNG)

The mods provided on our [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/) page are already structured accordingly and only need to be extracted into the mod directory folder as is.

Once added to the correct mod directory, simply right click the game again, select properties and activate the installed mod. The same process can be followed in reverse for de-activating mods

![](https://cdn.discordapp.com/attachments/512678820092968971/697124627520159804/Mods_on.PNG)

### **How do I install game updates or DLC?**
Installing updates and DLC is simple. In the top left corner of the emulator window, select `File / Install Files to NAND`, then select the file you wish to install. Once installed, your files should load automatically and the installed update or DLC will be shown in the games list add-ons column of the corresponding game.

If you wish to activate/deactivate a specific update or DLC then right click your game in the games list, select `Properties`, then enable or disable as needed.

![](https://cdn.discordapp.com/attachments/512678820092968971/697129823407177789/Updates_and_DLC.PNG)

### **How do I uninstall game updates or DLC?**

Due to current file system limitations, there is no easy way to uninstall a specific update/DLC.

It is usually easiest to just delete everything and then reinstall any updates and DLC that you need.

Installed updates/DLC are found in `%appdata%\yuzu\nand\user\Contents\registered\`.

To remove them, you will need to delete this `registered` folder.

_Remember to reinstall any updates or DLC you need._

Afterwards, go to `Settings / System / Filesystem tab` and click on `Reset Metadata Cache` on the bottom. This will refresh the games list addons column.

### **How do I set up my controls?**

Since the Nintendo Switch is a complicated device controller input wise, you will need to change some input settings depending on the game you wish to play.

In the input window dropdown, Select `Custom`, then click on `Configure`.

![](https://cdn.discordapp.com/attachments/356187763139280896/697133498074660904/Custom.PNG)

**For all games other than Pokemon Let's Go set the controls like this:**

![](https://cdn.discordapp.com/attachments/400106910231035904/690188034087714847/pro.png)

* Map your controls by clicking on `Configure` next to `Pro Controller`.
* Make sure to map your analog sticks by clicking on the `Set analog Stick` button if you are using a controller.
* Restart yuzu after you are done for the new settings to take effect.

**For Pokemon Let's Go set your controls like this:**

![](https://cdn.discordapp.com/attachments/400106910231035904/689931041720238097/PLG.png)

* Map your controls by clicking on `Configure` next to the `Joycons Docked` checkbox.
* Make sure `Player 1` is set to `None` as depicted in the screenshot.
* Make sure to map your analog sticks by clicking on the `Set analog Stick` button if you are using a controller.
* Restart yuzu after you are done for the new settings to take effect

### **How do I add a save to my Game**

To add a save, simply right-click your game in the Games List, Select `Open Save Data Location`, then Select your User from the Profile Selector

![](https://cdn.discordapp.com/attachments/356187763139280896/697140759454941245/User_list_saves.PNG)

Once your `Save Data Location` is open, place your game saves in this directory

![](https://cdn.discordapp.com/attachments/356187763139280896/697142111568527400/save_location.PNG)

### **yuzu closes when I try to open it**
Disconnect any USB gamepad you have and relaunch yuzu.

### Games fail to launch with the error: "WerFault.exe - Application Error - The application was unable to start correctly"

This typically occurs when yuzu runs out of RAM. Increase the size of your pagefile to resolve the issue.

### What is Boxcat?

Please read the following article: [Boxcat](https://yuzu-emu.org/help/feature/boxcat/)

### Why am I getting an error?

Please look up your error in the following page: [Error Codes](https://yuzu-emu.org/help/reference/error-codes/)

### What are Mods and how do I install them?

Please read the following article: [Mods](https://yuzu-emu.org/help/feature/game-modding/)

### How do I upload my log file?

Please read the following guide: [How to Upload the Log File](https://yuzu-emu.org/help/reference/log-files/)

### How do I use the resolution scanner?

**This is currently broken, and not working.**\
Please read the following guide: [How to Use the Resolution Scanner](https://yuzu-emu.org/help/feature/resolution-rescaler/)

### What is Telemetry?

Please read the following article: [What is Telemetry?](https://yuzu-emu.org/help/feature/telemetry/)

### How do I install Early Access?

Please read the following guide: [How to install Early Access](https://yuzu-emu.org/help/early-access/)

---

### **What is yuzu?**
yuzu is an experimental open-source emulator for the Nintendo Switch from the creators of Citra.
It is written in C++ with portability in mind, with builds actively maintained for Windows, Linux and macOS. The emulator currently can play various commercial titles and homebrew applications with varying degrees of success.

### **Which software license is yuzu licensed under?**
yuzu is an open-source project, licensed under the GPLv2 (or any later version). Refer to the license document for more information.

### **Which platforms does yuzu support?**
yuzu is actively tested and supported on various 64-bit versions of Windows (7 and up) and Linux. macOS is no longer supported due to Apple deprecating OpenGL.

### **What are the system requirements for yuzu?**
yuzu currently requires an OpenGL 4.5 capable GPU and a CPU that has high single-core performance. It also requires a minimum of 8 GB of RAM. For more details, see our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/#hardware).

### **How do I build yuzu for the OS that I use?**
Take a look at the following guides for steps on building yuzu for the following platforms:
  - [Linux](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Linux)
  - [Windows](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Windows)

### **Who made yuzu?**
yuzu has an active team of open-source developers. The list of contributors can be [found on GitHub](https://github.com/yuzu-emu/yuzu/graphs/contributors).