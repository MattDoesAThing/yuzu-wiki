 How to Dump Keys
 ================
 In order to play games in XCI or NCA format, you must have the required keys to decrypt them.

 ## Process
Guide on how to obtain the decryptions keys.

* Requirements: A hackable Nintendo Switch (you can check whether your Nintendo Switch is hackable or not [here.](https://akdm.github.io/ssnc/checker/))
* A Micro SD card of at least 1 Gigabyte in capacity.
* A Micro SD card reader.
* Lockpick: Is included by default in [Kosmos CFW](https://github.com/AtlasNX/Kosmos/releases) if you don’t use that you can download it [here.](https://github.com/shchmue/Lockpick/releases)
* The necessary tools (i.e a jig, paperclip, etc.) required to be able to boot into RCM and navigate around the [Hekate](https://github.com/CTCaer/hekate/releases) 
  menu.
* [TegraRCMGUI](https://github.com/eliboa/TegraRcmGUI/releases/download/2.5/TegraRcmGUI_v2.5_Installer.msi) or [TegraRCMSmash.](https://files.sshnuke.net/TegraRcmSmash1213.zip)

**You can skip to Step 3 if you already have CFW set-up.**
* **Step 1:** Turn off your Nintendo Switch and plug your Micro SD card into your computer.
* **Step 2:** Download the latest [Kosmos CFW](https://github.com/AtlasNX/Kosmos/releases) (If you already have that or use a different CFW software download the latest [Lockpick](https://github.com/shchmue/Lockpick/releases). and extract than in your “/switch/” folder) and extract the zip in the root of your Micro SD card.
* **Step 3:** Put your SD card back in your Nintendo Switch, boot into RCM mode and inject the latest Hekate payload * using your preferred payload injector.
* **Step 4a:** Using the touchscreen go to `Console info`.
* **Step 4b:** Select `Fuses` (not kfuse!) and press the `Dump fuses` button to save `fuses` to your Micro SD card.
* **Step 4c:** Return back to `Console info`  and select `TSEC Keys` and press the `Dump Keys` button to save `TSEC keys` to your Micro SD card.

**If you are on firmware 7.x and above you'll need to run the [Lockpick_RCM](https://github.com/shchmue/Lockpick_RCM/releases) payload instead.**

**For those above 7.x**
* **Step 5:** Go back to the hekate menu and go to **Payloads** and then pick Lockpick_RCM.bin.
* **Step 6:** After it's done running go to **Step 7**

**For the title.keys (and prod.keys for those under 7.x)**

* **Step 7:** Boot into your CFW of choice, and open the Homebrew Menu (Album application) while pressing the `R` button on your joy-con.
* **Step 8:** Navigate the menu and run Lockpick.
* **Step 9:** Once it says it's done turn you Nintendo Switch off and plug your Micro SD card into your computer.
* **Step 10:** Locate to the `/switch/` folder on your Micro SD card where you’ll find two .keys files; `prod.keys` and `title.keys`, copy these and paste them into the `&appdata&/yuzu/keys/` folder.

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
 
