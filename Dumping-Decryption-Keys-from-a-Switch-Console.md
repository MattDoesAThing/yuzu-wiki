 How to Dump Keys
 ================
 In order to play games in XCI or NCA format, you must have the required keys to decrypt them.

 ## Process
Guide on how to obtain the decryptions keys.

* Requirements: A hackable Nintendo Switch (you can check whether your Nintendo Switch is hackable or not [here.](https://akdm.github.io/ssnc/checker/))
* A Micro SD card of at least 1 Gigabyte in capacity.
* A Micro SD card reader.
* Lockpick: Is included by default in [Kosmos CFW](https://github.com/AtlasNX/Kosmos/releases) if you don’t use that you can download it [here.](https://github.com/shchmue/Lockpick/releases/download/v1.2.3/Lockpick.nro)
* The necessary tools (i.e a jig, paperclip, etc.) required to be able to boot into RCM and navigate around the [Hekate](https://github.com/CTCaer/hekate/releases/download/v4.10.1/hekate_ctcaer_4.10.1.zip) 
  menu.
* [TegraRCMGUI](https://github.com/eliboa/TegraRcmGUI/releases/download/2.5/TegraRcmGUI_v2.5_Installer.msi) or [TegraRCMSmash.](https://files.sshnuke.net/TegraRcmSmash1213.zip)

**You can skip to Step 3 if you already have CFW set-up.**
* **Step 1:** Turn off your Nintendo Switch and plug your Micro SD card into your computer.
* **Step 2:** Download the latest [Kosmos CFW](https://github.com/AtlasNX/Kosmos/releases) (If you already have that or use a different CFW software download the latest [Lockpick](https://github.com/shchmue/Lockpick/releases/download/v1.2.3/Lockpick.nro). and extract than in your “/switch/” folder) and extract the zip in the root of your Micro SD card.
* **Step 3:** Put your SD card back in your Nintendo Switch, boot into RCM mode and inject the latest Hekate payload * using your preferred payload injector.
* **Step 4a:** Using the **VOL** and **Power** buttons to navigate, select `Console info…`
* **Step 4b:** Select `Print fuse info` (not kfuse info!) and press the **Power** button to save `fuse info` to your Micro SD card.
* **Step 4c:** Return back to `Console info…`  and select `Print TSEC keys` and press the **Power** button to save `TSEC keys` to your Micro SD card.
* **Step 5:** Boot into your CFW of choice, and open the Homebrew Menu (Album application).
* **Step 6:** Run Lockpick.
* **Step 7:** Turn you Nintendo Switch off and plug your Micro SD card into your computer.
* **Step 8:** Locate to the `/switch/` folder on your Micro SD card where you’ll find two .keys files; `prod.keys` and `title.keys`, copy these and paste them into the `&appdata&/yuzu/keys/` folder.

And you’re done! Congratulations! You’ve just dumped your decryption and title keys!

Place it in:

 `C:/Users/yourusername/AppData/Roaming/yuzu/keys` _(for Windows)_
 
 `~/.local/share/yuzu-emu/keys` _(for macOS and Linux)_

##### Diagram showing the correct location of the decryption keys in yuzu's [[User Directory]].

```
"User Directory"
└── config
└── keys
    └─── prod.keys
    └─── title.keys
└── log
└── nand
└── sdmc
└── sysdata
```
Please seek support in the official yuzu discord server if you have any further issues.
If you have suggestions for this guide please contact me on discord @MysticExile#1552

Credits:

* **CTCaer** for maintaining Hekate
* **Rajkosto** for creating and maintaining TegraRCMSmash
* **AtlasNX** for creating and maintaining Kosmos CFW
* **shchmue** for creating and maintaining Lockpick
 
