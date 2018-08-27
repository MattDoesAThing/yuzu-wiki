In Short:
**Use XCIs for gamecards, NSPs for anything else. You need encryption keys which you can [dump with our guide](https://github.com/yuzu-emu/yuzu/wiki/Dumping-Decryption-Keys-from-a-Switch-Console)**

### Short Descriptions of Yuzu-supported Formats
- XCI: Represents a dump of a game cartridge. Contains icons, metadata, and a switch game. Sometimes contains updates to the game as well. *Used For:* Dumps of Gamecards you own
- NSP: Contains all of the files and data needed to display icons, a title and a game. 
*Used For*: Dumps of SD and NAND games, Updates
- NCA: A raw format that can contain a multitude of things (most similar to a ZIP file on your computer)
*Used For*: System Archives
- Deconstructed Rom Directory: An NCA that has been expanded into its component parts.
*Used For*: Developers and Power Users with more advanced applications
- NSO/NRO Homebrew: Cool and neat applications made unofficially by members of the community

### Here is an overall diagram of what each format contains:
![](https://cdn.discordapp.com/attachments/451185149032529930/482693990240485429/Switch_Game_Formats.jpg)