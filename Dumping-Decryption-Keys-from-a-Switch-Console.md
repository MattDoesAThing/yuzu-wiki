 How to Dump Keys
 ================
 In order to play games in XCI or NCA format, you must have the required keys to decrypt them.

 ## Process
 You will need to follow [**this**](https://gbatemp.net/threads/how-to-get-switch-keys-for-hactool-xci-decrypting.506978/) key dumping guide, however, in step 5 of the guide, you will need to rename your key file to `prod.keys`.
 
Place it in:

 `C:/Users/yourusername/AppData/Roaming/yuzu/keys` _(for Windows)_
 
 `~/.local/share/yuzu-emu/keys` _(for macOS and Linux)_

##### Diagram showing the correct location of the decryption keys in yuzu's [[User Directory]].

```
"User Directory"
└── config
└── keys
    └─── prod.keys
└── log
└── nand
└── sdmc
└── sysdata
```

**You're done!**