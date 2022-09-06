If you are unable to find the answer to your question, please join our Discord server for support: [Discord Server](https://discord.gg/u77vRWY)
### **Table of contents**
* [yuzu starts with the error “VCRUNTIME140_1.dll was not found”](#yuzu-starts-with-the-error-vcruntime140_1dll-was-not-found)
* [How do I get Games?](#how-do-i-get-games)
* [Can I use a Mariko Switch/Switch Lite/OLED Model for the dumping process?](#can-i-use-a-mariko-switchswitch-liteoled-model-for-the-dumping-process)
* [yuzu starts with the error "Broken Vulkan Installation Detected"](#yuzu-starts-with-the-error-broken-vulkan-installation-detected)
* [yuzu starts with the error "Missing Derivation Components"](#yuzu-starts-with-the-error-missing-derivation-components)
* [yuzu starts with the error "Unable to start application: Os { code: 2, kind: NotFound, message: “The system cannot find the file specified.” }"](#yuzu-starts-with-the-error-unable-to-start-application-os-code-2-kind-notfound-message-the-system-cannot-find-the-file-specified)
* [yuzu will not update further or starts with a Qt platform error](#yuzu-will-not-update-further-or-starts-with-a-qt-platform-error)
* [yuzu closes when opening Configure](#yuzu-closes-when-opening-configure)
* [My game is Lagging and Dropping to Low Framerates](#my-game-is-lagging-and-dropping-to-low-framerates)
* [How do I use mods or cheats?](#how-do-i-use-mods-or-cheats)
* [How do I install game updates or DLC?](#how-do-i-install-game-updates-or-dlc)
* [How do I uninstall game updates or DLC?](#how-do-i-uninstall-game-updates-or-dlc)
* [How do I set up my controls?](#how-do-i-set-up-my-controls)
* [How do I use my GameCube controller adapter?](#how-do-i-use-my-gamecube-controller-adapter)
* [How do I add a save to my Game](#how-do-i-add-a-save-to-my-game)
* [yuzu closes when launching game](#yuzu-closes-when-launching-game)
* [Games fail to launch with the error: "WerFault.exe - Application Error"](#games-fail-to-launch-with-the-error-werfaultexe---application-error---the-application-was-unable-to-start-correctly)
* [What is Boxcat?](#what-is-boxcat)
* [Why am I getting an error?](#why-am-i-getting-an-error)
* [What are Mods and how do I install them?](#what-are-mods-and-how-do-i-install-them)
* [How do I upload my log file?](#how-do-i-upload-my-log-file)
* [What is Telemetry?](#what-is-telemetry)
* [How do I install Early Access?](#how-do-i-install-early-access)
* [What is yuzu?](#what-is-yuzu)
* [Which software license is yuzu licensed under?](#which-software-license-is-yuzu-licensed-under)
* [Which platforms does yuzu support?](#which-platforms-does-yuzu-support)
* [What are the system requirements for yuzu?](#what-are-the-system-requirements-for-yuzu)
* [How do I build yuzu for the OS that I use?](#how-do-i-build-yuzu-for-the-os-that-i-use)
* [Who made yuzu?](#who-made-yuzu)


### **yuzu starts with the error “VCRUNTIME140_1.dll was not found”**

![](https://cdn.discordapp.com/attachments/512678820092968971/699336946698158120/VC_missing.png)

Could also show up as “MSVCP140_ATOMIC_WAIT.dll was not found”.

Current versions of yuzu require the latest versions of Microsoft Visual C++. Please download and install the following dependency:

https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads

Go to Visual Studio 2015, 2017 and 2019, and select the link next to x64.


### **How do I get games?**

You are legally required to dump your games from your Nintendo Switch. To do so, please follow our in-depth [Quickstart Guide](https://yuzu-emu.org/help/quickstart/).


### **Can I use a Mariko Switch/Switch Lite/OLED Model for the dumping process?**

Yes, but support for those models is beyond our scope since they require hardware-based modifications to load custom firmware. We still recommend obtaining a Switch console that is vulnerable to the `fusée-gelée` RCM exploit, as it's still the most accessible way for jailbreaking. To check if your Switch is hackable using this exploit, visit [Is My Switch Patched?](https://ismyswitchpatched.com) and enter your console’s serial number.


### **yuzu starts with the error "Broken Vulkan Installation Detected"**

This problem indicates that the Vulkan initialization failed on the previous boot of yuzu. Please perform the following:

* Update your graphics drivers
* Uninstall/update problematic screen-recording or overlay software
* Verify your Vulkan installation by navigating to Emulation > Configure > Graphics > Click "Check for Working Vulkan"

If issues persist, please reach out for support via our [Discord server](https://discord.gg/u77vRWY) or our [Forum](https://community.citra-emu.org/c/yuzu-support/14).


### **yuzu starts with the error "Missing Derivation Components"**
![](https://cdn.discordapp.com/attachments/512678820092968971/699337208443699307/Keys_missing.PNG)

yuzu requires console keys to play your games. Please follow our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/) to dump these keys and system files from your Nintendo Switch.

These console keys (prod.keys/title.keys) need to be placed in the following directories:

You may need to create the following "keys" folder:
* Windows: `C:\Users\USERNAME\AppData\Roaming\yuzu\keys`
* Linux: `/home/USERNAME/.local/share/yuzu/keys`

**NOTE: This yuzu directory can be quickly accessed by selecting file/open yuzu folder within the emulator**


### **yuzu starts with the error "Unable to start application: Os { code: 2, kind: NotFound, message: “The system cannot find the file specified.” }"**

![](https://cdn.discordapp.com/attachments/356187763139280896/709806101134049320/error_2.PNG)

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
* Note: Doing this will not touch your existing keys - saves for yuzu, as they reside in %appdata%\yuzu\ not localappdata yuzu folder.


### **yuzu closes when opening Configure**

This problem may be caused by a corrupt configuration file.
Press Win+R, type `%appdata%\yuzu\config` and delete the `qt-config.ini` file. Your global settings will be lost after doing this, reconfigure accordingly.

Alternatively, some screen recording applications use dubious methods to inject themselves into software, causing crashes. Some examples are Reshade, GShade, Bandicam, Action and Screenrec. Uninstall the software if you have it installed. For Reshade-GShade if you need to keep it installed at the very least turn off its ability to touch Vulkan globally on windows to allow Yuzu&Vulkan to work again.

We recommend using OBS Studio, Radeon ReLive, Nvidia ShadowPlay or Microsoft XBox Game Bar.

Overwolf is also a known cause of issues, we recommend avoiding it.


### **My game is Lagging and Dropping to Low Framerates**

You are likely experiencing Shader Caching. Shaders are small programs running on a graphic card, responsible for rendering graphics like terrain, explosions, characters, etc. Since a PC cannot directly execute switch shaders, it first has to translate them to a format a PC can understand. This translation process is time consuming, and you'll notice it in two ways:

* While playing, if yuzu needs to translate a new shader, the game will stutter. Loading into a game for the first time can give long freezes due to the number of shaders. As you keep playing, the amount of stuttering will decrease.

* When launching a game, the shader cache is loaded. To speed up this process there exists an additional "precompiled" cache. This cache may get reset every time you update yuzu or install a new GPU driver. The precompiled cache will then be compiled from scratch, causing a longer load time.

Vulkan and OpenGL have separate caches, but different OpenGL backends share the same cache. This means that on Nvidia you can build up shaders with less stutter on GLASM, then use GLSL for more performance.

**IMPORTANT: Since the cache stores parts of the game, we don't condone sharing or downloading these, since it is considered piracy.**


### **How do I use mods or cheats?**
For a list of useful mods for your favorite games, check our database with [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/)

To add mods to a specific game, simply right click the game in yuzu's games list, select `Open Mod Data Location` and structure your mod files similar to this example:

`Mod directory/mod name/romfs`
_or_
`Mod directory/mod name/exefs`

To add cheats, structure your cheat file similar to this example:

`Mod directory/cheat name/cheats`

An example of a correctly structured mod directory can be seen below:

![](https://cdn.discordapp.com/attachments/512678820092968971/697113928852963378/Mod_Format.PNG)

The mods provided on our [Switch Mods](https://yuzu-emu.org/wiki/switch-mods/) page are already structured accordingly and only need to be extracted into the mod directory folder as is.

Once added to the correct mod directory, simply right click the game again, select properties and activate the installed mod. The same process can be followed in reverse for de-activating mods

![](https://cdn.discordapp.com/attachments/512678820092968971/697124627520159804/Mods_on.PNG)


### **How do I install game updates or DLC?**
Installing updates and DLC is simple. In the top left corner of the emulator window, select `File / Install Files to NAND`, then select the file you wish to install. Once installed, your files should load automatically and the installed update or DLC will be shown in the games list add-ons column of the corresponding game.

If you wish to activate/deactivate a specific update or DLC then right click your game in the games list, select `Properties`, then enable or disable as needed.(See Below)

![](https://cdn.discordapp.com/attachments/512678820092968971/697129823407177789/Updates_and_DLC.PNG)

Reinstalling or Overwriting Updates/DLC is as simple as following the above instructions, selecting your files and installing your Update/DLC. When doing this, any previously installed files will be removed and replaced by the newly installed versions.


### **How do I uninstall game updates or DLC?**

To delete your installed game Updates or DLCs, right click your game, then select Remove. From here you can delete/uninstall your game Updates and DLCs from the options list (See Below)

![](https://cdn.discordapp.com/attachments/356187763139280896/739433965584384010/Remove_updates_and_DLC.PNG)


### **How do I set up my controls?**

Since the Nintendo Switch is a complicated device controller input wise, you will need to change some input settings depending on the game you wish to play.

Open the yuzu settings and go to `Controls`.

**For all games other than Pokemon Let's Go set the controls like this:**

![](https://cdn.discordapp.com/attachments/749020865626374244/749029883556135043/mjolnir_pro.gif)

* Click on the checkbox next to `Connect Controller` if it is not already checked.
* Select `Pro Controller` in the combobox below if needed (this is also the default).
* Select your desired input device under `Input Device`.
* Controllers: All buttons should automatically be mapped for the selected input device.
* Keyboard: The `Defaults` button on bottom right sets default keyboard mappings.
* Change mappings if desired.
* Repeat steps for other players if desired.
* Confirm with `OK`.

**For Pokemon Let's Go set your controls like this:**

![](https://cdn.discordapp.com/attachments/749020865626374244/749029890065432586/mjolnir_handheld.gif)

* Click on the checkbox next to `Connect Controller` if it is not already checked.
* Select `Handheld` in the combobox below.
* Select your desired input device under `Input Device`.
* Controllers: All buttons should automatically be mapped for the selected input device.
* Keyboard: The `Defaults` button on bottom right sets default keyboard mappings.
* Change mappings if desired.
* Confirm with `OK`.


### **How do I use my GameCube controller adapter?**

The GameCube adapter communicates with yuzu over the `libusb` protocol. This works natively on Linux, but requires the installation of a compatible driver on Windows using Zadig.


#### Zadig driver installation
Plug in the GameCube controller adapter if it hasn't been already. Download and launch [Zadig](https://zadig.akeo.ie/). 
If you're using the Mayflash adapter, make sure you switch it to `Wii U` or Zadig won't pick it up properly.

1. From the `Options` menu in Zadig, select `List All Devices`

2. In the pulldown menu, select `WUP-028`. Ensure that its USB ID is `057E 0337`.

* If it does not appear in the list then try inserting the adapter (specifically its black USB cord) into another USB port.

3. On the right column, select `WinUSB` then click `Replace Driver`. Select `Yes` to modify the system driver.

When the notification that the driver is installed successfully is displayed, you can close Zadig and continue to configuring the controller with yuzu.


#### GameCube controller configuration

Ensure the adapter is plugged in prior to launching yuzu. Then follow the [How do I set up my controls?](#how-do-i-set-up-my-controls) instructions, selecting `Gamecube controller X` as the `Input Device`, where `X` is the port in which the controller is plugged into.

![](https://cdn.discordapp.com/attachments/737476434536431737/760951986417172520/gc_automap.png)


### **How do I add a save to my Game**

To add a save, simply right-click your game in the Games List, Select `Open Save Data Location`, then Select your User from the Profile Selector

![](https://cdn.discordapp.com/attachments/356187763139280896/697140759454941245/User_list_saves.PNG)

Once your `Save Data Location` is open, place your game saves in this directory

![](https://cdn.discordapp.com/attachments/356187763139280896/697142111568527400/save_location.PNG)


### **yuzu closes when launching game**

* If you happen to have issue launching game and have Nod32 ESET Antivirus installed. Please uninstall it and reboot. Or add yuzu into the HIPS exclusions. It is known to cause issue with emulators recently.
* Example adding exception below
![image](https://user-images.githubusercontent.com/23653025/178130047-be87687b-54ae-410e-aabd-ad843406d14f.png)
![image](https://user-images.githubusercontent.com/23653025/178130025-254491e6-a568-4f79-8c4c-b9353a624667.png)


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


### What is Telemetry?

Please read the following article: [What is Telemetry?](https://yuzu-emu.org/help/feature/telemetry/)


### How do I install Early Access?

Please read the following guide: [How to install Early Access](https://yuzu-emu.org/help/early-access/)


---

### **What is yuzu?**

yuzu is an experimental open-source emulator for the Nintendo Switch from the creators of Citra.
It is written in C++ with portability in mind, with builds actively maintained for Windows and Linux. The emulator currently can play various commercial titles and homebrew applications with varying degrees of success.


### **Which software license is yuzu licensed under?**

yuzu is an open-source project, licensed under the GPLv2 (or any later version). Refer to the license document for more information.


### **Which platforms does yuzu support?**

yuzu is actively tested and supported on various 64-bit versions of Windows (10 and up) and Linux. macOS is no longer supported due to Apple deprecating OpenGL.


### **What are the system requirements for yuzu?**

yuzu currently requires an OpenGL 4.6 capable GPU and a CPU that has high single-core performance. It also requires a minimum of 8 GB of RAM. For more details, see our [Quickstart Guide](https://yuzu-emu.org/help/quickstart/#hardware).


### **How do I build yuzu for the OS that I use?**

Take a look at the following guides for steps on building yuzu for the following platforms:
  - [Linux](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Linux)
  - [Windows](https://github.com/yuzu-emu/yuzu/wiki/Building-for-Windows)


### **Who made yuzu?**

yuzu has an active team of open-source developers. The list of contributors can be [found on GitHub](https://github.com/yuzu-emu/yuzu/graphs/contributors).