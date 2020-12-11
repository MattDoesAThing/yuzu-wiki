## How to Install Updates

- If you have an update in NCA format, click `File`, then `Install file to NAND...`, select your update NCA, and then in the drop down box select `Game Update`. If you get an error, double check you encryption keys and dump.
- If you have updates installed on your NAND or SD card, you can copy the entire NAND into `%YUZU_DIR%/nand/user` or the entire sd card to `%YUZU_DIR%/sdmc`.
- If your update is in NSP format, use the File > Install File method described above for NCA, except the `Game Update` menu won't show (yuzu can infer it from the NSP metadata)

## Using Updates

- If your update was installed successfully, next to all games that match the title ID of the update, a message will show in the add-ons column of the gamelist.
    - If you installed just an update NCA, it will probably only say `Update`.
    - If you copied your NAND or SD or used an NSP update, it will probably say `Update vX.Y.Z` where X, Y, and Z are numbers. Don't be alarmed if the numbers don't match what the game says the version is, the version in the game list is the version as determined by Nintendo's servers, the one in game is independent.
- Updates do *not* apply to deconstructed ROM directories (folder with `main`, `main.npdm`, `game.romfs`, etc). This is because the romfs cannot be guaranteed to be the base game, and patching anything else will result in strange bugs and crashes. If you can guarantee that your romfs is the base game, skip to the [Repacking to NSP](#repacking-to-nsp) section to force yuzu to patch it.

## Repacking to NSP

- If you only have games in directory format, and re dumping is not an option (it's much easier/safer), and you can guarantee that the romfs hasn't been updated or modified in any way, then you can trick yuzu into patching it. First download this [python script](https://github.com/CVFireDragon/nspBuild/releases/latest). You will need Python to execute it. Then copy it to the romfs directory and execute the following in command prompt: `python nspBuild.py out.nsp ...` where ... are the names of all the game files in the dir (`main`, `main.npdm`, `sdk`, `rtld`, `subsdk*`, and `game.romfs`). Then `out.nsp` will contain your packed games and updates will apply to it.

## Adding a Version Number to NCA Updates
**WARNING: For advanced users only**
- Go to `%YUZU_DIR%/nand/user/yuzu_meta`. Find the file called `Patch_<>.cnmt` where <> is the title ID of the update. Open this file in a hex editor. Edit the four bytes starting at offset 0x8 to the version you want. This is a LE u32 value. To remove this custom version, make the value 0.