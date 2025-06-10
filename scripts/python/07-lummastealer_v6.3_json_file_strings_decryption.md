# LummaStealer v6.3 json file strings decryption

```python

import base64
import json

recive_message_enc = json.loads("""
{
    "v": 4,
    "se": true,
    "ad": false,
    "vm": false,
    "ex": [
        {
            "en": "Ci1CgzXEg0FvLSiDV8TiQWYtIINUxOhBZS0yg1nE4EFiLS6DUsTrQW8tIYNRxOJBZi0vg1DE5kFvLSODX8TtQWMtL4NdxO5B",
            "ez": "Ci1CgzXEg0FHLSeDQcTiQUctI4NGxOhB"
        },
        {
            "en": "Ci1CgzXEg0FrLSeDV8TvQWwtJoNexOtBYi0qg1HE4EFuLSiDRcTqQWwtKoNdxOFBbi0rg1rE6UF6LS6DU8TpQWQtIYNaxOJB",
            "ez": "Ci1CgzXEg0E7LRKDVMTwQXktNYNaxPFBbi0="
        },
        {
            "en": "Ci1CgzXEg0FgLSyDWcTkQWstL4NQxOBBaC0yg1jE4UFrLSiDX8TlQWItL4NYxO5BZi0qg1DE6UFhLSeDWMTmQWAtJoNYxOJB",
            "ez": "Ci1CgzXEg0FILTCDVMTiQXwtLYNGxA=="
        },
        {
            "en": "Ci1CgzXEg0FuLS6DVsTsQWgtMoNfxOpBYy0lg0XE6kFhLS2DWsThQWUtKoNYxOJBaC0ng13E60FnLSqDU8TsQWUtJoNXxOFB",
            "ez": "Ci1CgzXEg0FLLSWDR8TmQWQtNoMVxNtB"
        },
        {
            "en": "Ci1CgzXEg0FgLSWDVMTiQWMtL4NUxOlBYy0yg1fE80FuLS2DUsTzQW4tJYNZxOtBay0yg13E70FuLSODXsTqQWEtJYNQxOVB",
            "ez": "Ci1CgzXEg0FJLS2DXMTtQWItN4NXxA=="
        },
        {
            "en": "Ci1CgzXEg0FsLSGDU8TgQWwtLoNZxOVBZC0mg1nE7EFnLSaDXcThQW8tKoNfxOlBaS0tg1zE7kFoLSWDWsTlQW4tLINWxORB",
            "ez": "Ci1CgzXEg0FGLSeDVMTzQSotFYNUxO9BZi0ng0HE"
        },
        {
            "en": "Ci1CgzXEg0FmLSWDWMTzQWktMoNSxO9Bei0sg1LE50FlLSODWcThQW0tJ4NaxO9Bbi0ng1TE6UFsLSGDWcTtQWItI4NTxOJB",
            "ez": "Ci1CgzXEg0FZLSODU8TmQXotI4NZxA=="
        },
        {
            "en": "Ci1CgzXEg0FiLSaDWsToQWMtJ4NfxO1Bei0rg1jE4kFhLSeDUcTrQWstKINdxOdBZi0hg1DE5EFvLTKDWcTqQWUtI4NdxOdB",
            "ez": "Ci1CgzXEg0FGLSODRsT3QVotI4NGxPBB"
        },
        {
            "en": "Ci1CgzXEg0FhLSiDWMTsQWUtKoNZxORBZS0pg1bE4EFlLSaDXMTgQWAtKINTxOZBaC0kg1rE7kFmLSCDWcTpQW0tJINdxOhB",
            "ez": "Ci1CgzXEg0FYLS2DW8TqQWQtYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FrLSCDWsTkQWctK4NaxOBBZC0sg1DE5kFuLS+DWMTmQXotLINaxOtBZC0qg1nE6kFgLSGDX8TzQWktK4NTxOdB",
            "ez": "Ci1CgzXEg0FILS6DVMTnQW8tYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0F6LSuDWsTgQWYtMoNaxPNBZi0hg1HE4UFrLSeDU8TqQWItI4NYxOlBZS0qg1vE5kFsLSCDXMToQWAtK4NZxOBB",
            "ez": "Ci1CgzXEg0FPLTSDUMTxQWQtLYNBxOZB"
        },
        {
            "en": "Ci1CgzXEg0FuLSyDUsTuQWYtIINZxOBBZS0mg1PE7EFoLTKDUcTzQW8tIYNUxOJBbi0lg1PE4UFpLSWDUsTlQWAtJINbxO5B",
            "ez": "Ci1CgzXEg0FHLTeDWcT3QWMtNINQxPFBeS0agxXE1EFrLS6DWcTmQX4t"
        },
        {
            "en": "Ci1CgzXEg0FhLTKDRcTlQW4tK4NcxPNBei0qg1PE4EFpLSeDWMTgQWMtJYNbxOtBYy0kg0XE6UFhLSODRcTlQWgtK4NdxOdB",
            "ez": "Ci1CgzXEg0FMLS2DR8TtQWMtNoNQxPFBXS0jg1nE70FvLTaD"
        },
        {
            "en": "Ci1CgzXEg0FnLS+DWMTpQWgtIYNTxOxBbC0hg1rE7UFhLSODW8TtQWAtLYNbxOVBZy0og1\\/E4kFgLTKDWcTvQW4tJoNXxORB",
            "ez": "Ci1CgzXEg0FMLS6DQMT1QWMtYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FmLS2DXMTtQW8tKYNWxOJBaC0qg1nE7kFiLSiDX8ThQWUtIYNcxOlBbi0tg1zE7kFnLSeDX8TiQWQtJYNaxOJB",
            "ez": "Ci1CgzXEg0FNLS6DVMTwQXktYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FiLSeDUMTlQWUtKoNUxOVBbC0tg1jE6EFhLSmDRcTrQWQtLoNFxOxBYi0lg1nE7UFtLS+DV8TgQWktLoNdxOpB",
            "ez": "Ci1CgzXEg0FHLS2DR8TzQWItK4NGxKNBXS0jg1nE70FvLTaD"
        },
        {
            "en": "Ci1CgzXEg0FjLSaDW8TtQWgtJoNFxO9BZy0yg13E80FsLS6DU8TtQWYtKYNaxO5BbS0yg1PE4UF6LSGDUsTmQWYtLYNFxORB",
            "ez": "Ci1CgzXEg0FSLRSDUMTxQXktJ4MVxNRBay0ug1nE5kF+LQ=="
        },
        {
            "en": "Ci1CgzXEg0FrLSyDWsToQW0tL4NFxOtBZC0hg0XE5kFhLSmDXcTgQWYtL4NcxO1BbS0yg1zE7kFgLS+DVsTsQWUtK4NTxOFB",
            "ez": "Ci1CgzXEg0FJLS2DWMTzQWstMYMVxNRBay0ug1nE5kF+LQ=="
        },
        {
            "en": "Ci1CgzXEg0FpLSyDW8TgQWctJoNdxOlBay0hg0XE6EFnLSiDWMToQWktI4NTxOBBYi0yg0XE4UFkLTKDW8TrQW4tL4NaxO1B",
            "ez": "Ci1CgzXEg0FCLSODQ8TiQWItYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FlLSGDX8TnQXotL4NaxOJBZi0ug1jE5EFnLSiDV8ThQWUtJYNTxOpBYy0jg1rE5UF6LSqDV8TpQW0tIYNdxOtB",
            "ez": "Ci1CgzXEg0FZLTeDXMSjQV0tI4NZxO9Bby02gw=="
        },
        {
            "en": "Ci1CgzXEg0FlLSiDUsTkQWctIYNdxO9BbS0qg1vE6UFmLSODRcTuQWwtIINbxOlBYi0tg1nE5UFgLSmDXMTqQW4tIINWxOtB",
            "ez": "Ci1CgzXEg0FcLSeDW8TsQWctYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FkLSmDV8TqQWItJINXxOZBZS0lg1TE5kFrLS2DUMTrQWYtJ4NTxO1BYS0tg1HE4UFvLSSDUsTzQW0tKYNbxO1B",
            "ez": "Ci1CgzXEg0FHLSeDQcTiQUctI4NGxOhB"
        },
        {
            "en": "Ci1CgzXEg0FvLSWDX8TqQW4tKINXxPNBbS0ug1zE4EFiLSaDVsTsQWQtJoNXxOBBaC0mg1vE4UFvLSeDRcTzQW0tJoNFxOtB",
            "ez": "Ci1CgzXEg0FeLTCDQMTwQX4tYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FjLSCDW8TmQWAtJoNTxOlBZy0vg17E80FpLSyDWcTzQW8tIINexO9BZy0sg17E7EFvLS2DXMTrQWUtJINQxOBB",
            "ez": "Ci1CgzXEg0FeLTCDWsTtQUYtK4NbxOhB"
        },
        {
            "en": "Ci1CgzXEg0FsLSyDX8TrQWctKYNdxOtBZy0pg1fE6UFhLSmDVMThQWQtJoNWxO1BZC0tg1LE4kFtLS2DUsThQWQtJ4NQxOBB",
            "ez": "Ci1CgzXEg0FYLS2DW8TqQWQtYoNixOJBZi0ug1DE90E="
        },
        {
            "en": "Ci1CgzXEg0FnLSGDWsTrQWMtLoNbxOBBaC0kg1TE60FoLS+DUsTnQWAtKYNXxPNBby0vg1bE4EFjLSuDWsTvQW0tIYNSxOZB",
            "ez": "Ci1CgzXEg0FFLQmDbcQ="
        },
        {
            "en": "Ci1CgzXEg0FsLSqDV8TsQWItK4NYxOJBby0ug1fE7EFiLTKDX8ThQWgtLoNRxOBBZC0lg1bE7UFrLTKDW8TnQWUtJoNfxPNB",
            "ez": "Ci1CgzXEg0FILSuDW8TiQWQtIYNQxKNBSS0qg1TE6kFkLWKDYsTiQWYtLoNQxPdB"
        },
        {
            "en": "Ci1CgzXEg0FsLSSDW8ThQW8tLoNTxOdBZS0ng1zE7EFiLSeDW8ToQWAtK4NXxO1BZy0jg1HE6UFjLSeDXcTpQWItI4NfxOFB",
            "ez": "Ci1CgzXEg0FTLS2DR8TsQWMt"
        },
        {
            "en": "Ci1CgzXEg0FgLSCDUcTiQWUtIYNbxOZBYy0rg1zE7UFnLSiDV8TpQWYtJYNUxO9BYi0hg1DE70FtLSCDUMTpQWctLINcxOdB",
            "ez": "Ci1CgzXEg0FELSuDU8T3QXMt"
        },
        {
            "en": "Ci1CgzXEg0FrLSSDV8TgQWgtKINFxOFBei0kg1TE50FmLSmDWMTrQWctIYNZxOtBYS0ng1DE7EFuLS+DVMTuQWktJINZxOBB",
            "ez": "Ci1CgzXEg0FHLSODQcTrQQ=="
        },
        {
            "en": "Ci1CgzXEg0FiLSyDU8TiQWQtKYNbxOxBaS0kg1DE7EFsLSCDUcTnQW0tIYNcxOlBZC0vg13E7UFsLSyDXsTnQWQtI4NUxOdB",
            "ez": "Ci1CgzXEg0FJLS2DXMTtQWgtI4NGxOZB",
            "ldb": true
        },
        {
            "en": "Ci1CgzXEg0FiLTKDUsTvQWwtKoNSxOVBZC0qg1fE5EF6LSiDUcTmQWQtKINSxO5Bbi0lg1rE5kFjLSODRcTzQWstJINZxO1B",
            "ez": "Ci1CgzXEg0FNLTeDVMTxQW4tI4M="
        },
        {
            "en": "Ci1CgzXEg0FoLS6DW8TqQW8tK4NcxOVBbC0gg1rE6kFmLS6DXsTtQWAtLINQxPNBZS0lg1\\/E60FhLSWDW8TsQWstMoNUxOBB",
            "ez": "Ci1CgzXEg0FPLRODYMTCQQ=="
        },
        {
            "en": "Ci1CgzXEg0FpLSiDUMTvQWwtMoNZxPNBZi0ng1fE50FgLSiDUMTtQWYtLoNFxOlBaS0gg1nE7kFgLSmDU8TgQWwtJINbxOZB",
            "ez": "Ci1CgzXEg0FALSODTcT7QSotDoNcxOFBby0wg0HE+kE="
        },
        {
            "en": "Ci1CgzXEg0FsLSuDXcToQWstKYNTxOxBaC0pg1jE6EFgLS2DX8TzQWktKoNFxOVBbS0hg1jE60FsLSiDW8TuQWQtJINFxOpB",
            "ez": "Ci1CgzXEg0FILSuDQcTCQXotMoM="
        },
        {
            "en": "Ci1CgzXEg0FhLSyDVsTgQWItJoNcxORBZS0gg1LE60FvLSyDV8ThQWstJoNRxOxBYC0og1vE7UFrLS2DUsTlQXotMoNTxOlB",
            "ez": "Ci1CgzXEg0FjLRWDWcT3QQ=="
        },
        {
            "en": "Ci1CgzXEg0FhLSmDRcTvQWYtKYNaxOdBYC0ng1nE7EFjLSaDXMTmQW8tJoNaxOlBZS0lg1TE4EFsLSqDRcTiQWMtKoNaxOtB",
            "ez": "Ci1CgzXEg0FPLSyDfsTxQXMtMoNBxA=="
        },
        {
            "en": "Ci1CgzXEg0FrLS+DXsTuQWAtKINYxO5BbC0ug1HE50FlLSWDWMTrQXotKINZxOxBYy0vg1zE80FoLS2DU8TtQWwtKINcxOtB",
            "ez": "Ci1CgzXEg0FdLS2DWMThQWstNoM="
        },
        {
            "en": "Ci1CgzXEg0FkLS6DV8TuQWQtLINcxOlBaS0sg1nE5kFtLSmDX8TpQXotIYNTxOlBaS0ug1jE4EFsLSWDUsTlQW8tJINRxO5B",
            "ez": "Ci1CgzXEg0FHLQeDYsSjQUktGoM="
        },
        {
            "en": "Ci1CgzXEg0FkLSODW8TpQWctJoNexO1BYi0pg1zE7UFjLSSDW8ToQW0tJoNWxORBbS0hg1PE7UFiLSaDVMTiQWctL4NYxOlB",
            "ez": "Ci1CgzXEg0FNLTeDXMTvQW4t"
        },
        {
            "en": "Ci1CgzXEg0FkLSmDUcTnQW0tLINWxOdBYC0lg1\\/E5UFpLSaDUcTiQWctJINSxOBBZy0kg1vE70FiLSGDVsTtQWMtL4NcxORB",
            "ez": "Ci1CgzXEg0FZLSODQcT2QXgtLIM="
        },
        {
            "en": "Ci1CgzXEg0FpLTKDXcTrQWYtJYNYxORBay0vg1DE7EFuLSyDXcToQWAtJoNYxOhBei0jg1vE70FvLS6DW8TvQWUtKoNUxOxB",
            "ez": "Ci1CgzXEg0FELSeDWsTPQWMtLINQxA=="
        },
        {
            "en": "Ci1CgzXEg0FkLSqDW8ToQWgtKYNSxOlBYy0pg1LE4EFjLSWDVMTnQWUtL4NexPNBYi0jg1nE4kFkLSyDUcTgQWstMoNfxOhB",
            "ez": "Ci1CgzXEg0FJLS6DWsT1QW8tMIM="
        },
        {
            "en": "Ci1CgzXEg0FrLSGDWMTiQWktLYNRxOhBYC0gg1HE5EFnLS2DWcTmQW8tIINaxO9BZy0mg1\\/E7EFkLSuDWcToQW4tIINWxOtB",
            "ez": "Ci1CgzXEg0FYLSODV8ThQXMt"
        },
        {
            "en": "Ci1CgzXEg0F6LSqDXsThQWstL4NQxOVBYy0sg1LE5EFnLSODXsTkQWEtLoNFxOhBZi0og1\\/E7kFtLSuDV8TsQWItLINXxOJB",
            "ez": "Ci1CgzXEg0FaLS2DW8T3QW8tL4M="
        },
        {
            "en": "Ci1CgzXEg0FvLSSDV8TkQWYtJYNaxOVBZS0rg0XE80FoLSWDVsTpQW8tMoNbxOtBYy0gg1nE4kFjLSCDVsTtQWktLoNSxOhB",
            "ez": "Ci1CgzXEg0FHLSODR8T3QWMtI4NbxA=="
        },
        {
            "en": "Ci1CgzXEg0FkLSyDUsTgQW8tIYNexOFBay0yg1DE4UFsLSuDWMTtQWYtLINcxOpBYy0jg13E6EFrLSyDUcTgQWYtIINZxOFB",
            "ez": "Ci1CgzXEg0FILSuDQcT0QWstMINRxOZBZC0="
        },
        {
            "en": "Ci1CgzXEg0FmLTKDU8TgQWgtKINexO1BYy0og0XE5kFvLSuDWcTvQWMtJINbxOhBYy0pg1LE7UFpLSuDXsTkQWwtKoNRxOxB",
            "ez": "Ci1CgzXEg0FELSODWMTqQQ=="
        },
        {
            "en": "Ci1CgzXEg0FvLSiDX8TvQWstJoNcxO1BZC0hg17E50FtLSiDUMTuQW8tKYNQxOFBbi0yg1DE7EFhLSCDXMToQWItJINWxOpB",
            "ez": "Ci1CgzXEg0FaLSeDQcTxQWst"
        },
        {
            "en": "Ci1CgzXEg0FlLTKDVsTkQXotJINYxOpBei0rg1HE4UFtLTKDUMTtQWItL4NUxOlBZS0jg1\\/E80FoLS2DV8TzQXotJoNcxO9B",
            "ez": "Ci1CgzXEg0FZLTeDXMQ="
        },
        {
            "en": "Ci1CgzXEg0FrLSqDWsTvQXotJINRxOpBay0ug1\\/E5EFgLSSDXcTsQWctK4NdxOhBYC0gg1jE5EFgLSuDUcTvQWktJoNbxOxB",
            "ez": "Ci1CgzXEg0FPLTqDWsTnQX8tMYNixOZBaC1xgw=="
        },
        {
            "en": "Ci1CgzXEg0FlLSyDXcTsQW0tJINfxOZBay0hg1vE5UFlLS2DU8ToQWwtJYNFxPNBbi0ug1fE7kFmLS+DW8TzQWYtJYNXxO1B",
            "ez": "Ci1CgzXEg0FZLTeDV8Q="
        },
        {
            "en": "Ci1CgzXEg0FnLS2DRcTtQWctIINWxOJBbC0rg1DE50FuLSGDVMTkQWstJYNRxOBBaC0sg13E5kFgLSqDWcTsQW4tJINRxOdB",
            "ez": "Ci1CgzXEg0FaLS2DWcToQWstJoNaxPdBQC0Rgw=="
        },
        {
            "en": "Ci1CgzXEg0FsLSuDX8TtQW0tKINSxOBBYC0qg1\\/E7kFnLTKDVsTuQWEtJ4NcxOxBZy0ug1LE70F6LSeDXMTqQWAtKYNZxOdB",
            "ez": "Ci1CgzXEg0FeLSODWcTqQXktL4NUxO1B"
        },
        {
            "en": "Ci1CgzXEg0FiLSuDU8TiQWwtJYNYxOBBaS0mg0XE5kFhLTKDWcTsQWctKINfxOhBaS0kg1LE7EFuLSyDXcTgQW8tLoNZxOlB",
            "ez": "Ci1CgzXEg0FJLTCDTMTzQX4tLYN2xOxBZy0="
        },
        {
            "en": "Ci1CgzXEg0FhLTKDU8TsQXotKYNQxO9BZy0jg0XE4EFlLSuDRcTmQWctJINQxO1Bbi0vg1HE4EFtLSqDW8TmQW0tK4NYxO1B",
            "ez": "Ci1CgzXEg0FGLSuDRMT2QWstLoNcxPdBcy0="
        },
        {
            "en": "Ci1CgzXEg0FrLSuDXMTlQWgtLINXxOVBZS0gg0XE7kFvLSeDXsTqQXotKoNQxOZBYy0og1zE7kFuLTKDW8TvQXotJYNFxPNB",
            "ez": "Ci1CgzXEg0FeLSeDR8TxQWstYoNmxPdBay02g1zE7EFkLQ=="
        },
        {
            "en": "Ci1CgzXEg0FuLS+DXsTiQWctIYNexO1BZS0lg17E5EFpLSaDU8TrQWItIINRxOdBaS0lg13E4kFpLSqDXsTmQWAtJ4NUxPNB",
            "ez": "Ci1CgzXEg0FBLSeDRcTvQXgt"
        },
        {
            "en": "Ci1CgzXEg0FsLSqDWMTlQW8tLINRxORBbi0tg1bE7kFpLSCDWMTlQWMtKYNRxOBBZS0lg1rE5UF6LSqDXMTuQWQtKYNbxOxB",
            "ez": "Ci1CgzXEg0FZLS2DWcTvQW8tNoM="
        },
        {
            "en": "Ci1CgzXEg0FpLSyDWMTiQWctI4NUxOBBYi0yg0XE7UFhLSiDUsTtQWMtLoNRxPNBbi0vg17E4kFrLSmDUMTpQWQtKoNUxOZB",
            "ez": "Ci1CgzXEg0FLLTeDR8TsQQ=="
        },
        {
            "en": "Ci1CgzXEg0FgLS2DX8TrQWwtJ4NaxOZBbi0pg0XE6EFtLS6DV8TlQWMtL4NRxOVBay0gg0XE50FsLSiDVMTsQWUtLoNUxOVB",
            "ez": "Ci1CgzXEg0FaLS2DWcT6QWctJ4NGxOtB"
        },
        {
            "en": "Ci1CgzXEg0FsLS6DRcTqQWktK4NcxO9Bby0vg1LE60FoLS+DU8TiQWYtK4NWxOJBYC0tg1rE70FiLSmDXsTmQWQtJINQxA==",
            "ez": "Ci1CgzXEg0FDLQGDesTNQW8tOoM="
        },
        {
            "en": "Ci1CgzXEg0FkLSmDW8TrQWMtJ4NdxO9BYS0ug1zE80F6LSODU8TiQWEtI4NQxOhBZi0gg1DE5EFmLSeDVsTqQWwtKoNUxOdB",
            "ez": "Ci1CgzXEg0FELSODV8TsQXIt"
        },
        {
            "en": "Ci1CgzXEg0FiLSGDU8TvQXotK4NbxOBBei0yg0XE50FpLS6DXMTtQW8tI4NZxO5Bay0sg1HE6kFgLSGDWMTtQWEtIINSxO1B",
            "ez": "Ci1CgzXEg0FBLQqDdsQ="
        },
        {
            "en": "Ci1CgzXEg0FlLS2DXsTpQWYtIINexOpBYy0og1zE7UFiLTKDWMTtQWAtJINTxOBBZS0kg1\\/E7EFkLSCDU8ThQW0tI4NaxOBB",
            "ez": "Ci1CgzXEg0FeLSeDWMTzQWYtJ4M="
        },
        {
            "en": "Ci1CgzXEg0FnLSyDU8TqQWwtJ4NTxOhBay0og1LE7EFsLSmDVsTpQWEtJ4NYxOpBbi0rg1TE5kFpLS2DVsTtQWEtKINQxOtB",
            "ez": "Ci1CgzXEg0FeLSeDT8TBQWUtOoM="
        },
        {
            "en": "Ci1CgzXEg0FmLS2DUcTgQWktKINfxOFBbi0qg1PE4kFhLSODUMToQW4tK4NUxOtBZy0ng1HE5UFoLSuDUMTvQW4tJYNcxOhB",
            "ez": "Ci1CgzXEg0FOLQODRcTzQVotLoNUxPpB"
        },
        {
            "en": "Ci1CgzXEg0FjLSiDWMTzQW0tKYNfxOVBYS0gg1PE60FlLSeDV8TkQWUtJYNTxO9BbC0ng1fE7UFnLSeDX8TuQWwtIINYxA==",
            "ez": "Ci1CgzXEg0FILSuDQcTAQWYtK4NFxA=="
        },
        {
            "en": "Ci1CgzXEg0FmLSmDVsTpQWYtLINfxOVBei0gg1zE6EFnLSGDWMThQWstIYNdxOlBei0mg1fE6kFgLSeDX8TlQWYtMoNWxO5B",
            "ez": "Ci1CgzXEg0FZLTaDUMTmQWctYoN+xOZBcy0hg13E4kFjLSyD"
        },
        {
            "en": "Ci1CgzXEg0FlLSyDWsTlQXotLINXxOFBYS0ng13E80FnLS+DWsTiQWgtJYNFxOBBei0vg1zE5EFrLSSDWMTuQWQtKINdxA==",
            "ez": "Ci1CgzXEg0FELSODRsTrQSotB4NNxPdBby0sg0bE6kFlLSyD"
        },
        {
            "en": "Ci1CgzXEg0FoLSGDWsTzQW0tIYNdxOtBZS0og1jE5EFtLS+DU8TlQWMtLoNFxO9BZy0gg1HE6kFpLSWDVMTqQWItLoNexPNB",
            "ez": "Ci1CgzXEg0FCLTuDVsTsQWQtYoN5xOpBfi0ngxXEwEFmLSuDUMTtQX4t"
        },
        {
            "en": "Ci1CgzXEg0FhLS6DW8TiQW8tKINfxORBaC0rg1fE7kFiLS6DUMTzQWItLINdxPNBZy0jg1rE5UFlLSqDUsToQXotJYNexOdB",
            "ez": "Ci1CgzXEg0FQLSuDWcTTQWstO4M="
        },
        {
            "en": "Ci1CgzXEg0FrLSeDVMTgQWItKYNbxO5Bby0kg0XE60FvLTKDVsTgQWMtLYNbxOFBZS0tg13E4EFhLS2DW8TsQW8tJ4NYxORB",
            "ez": "Ci1CgzXEg0FJLS2DXMTtQTMteoM="
        },
        {
            "en": "Ci1CgzXEg0FoLSqDUsTrQWUtI4NYxOJBei0hg1HE80FoLS2DXcTzQWItK4NSxOxBZS0tg1TE50FuLSuDW8TzQWEtIINUxOpB",
            "ez": "Ci1CgzXEg0FLLTeDQcTrQW8tLINBxOpBaS0jg0HE7EF4LQ==",
            "ses": true
        },
        {
            "en": "Ci1CgzXEg0FuLSmDUcTmQW4tLoNFxORBbi0vg1jE6EFhLSSDX8TiQWgtJINTxOZBbS0jg1vE6kFvLSODWMTlQWEtLoNexO5B",
            "ez": "Ci1CgzXEg0FJLTuDVMTtQWUt"
        },
        {
            "en": "Ci1CgzXEg0FkLS6DUsThQWItJoNTxORBbi0qg1LE4UFjLSODWMTlQW4tJINYxOFBYy0pg1bE50FtLSqDXMTnQWUtI4NRxOdB",
            "ez": "Ci1CgzXEg0FILTuDWsTtQW8t"
        },
        {
            "en": "Ci1CgzXEg0FjLSyDU8TmQWgtLYNUxOlBbS0kg13E5EFoLSiDRcTpQWgtJ4NFxPNBaC0pg1LE7UFrLSCDU8TnQWEtJoNUxOVB",
            "ez": "Ci1CgzXEg0FFLSyDUMTIQW8tO4M="
        },
        {
            "en": "Ci1CgzXEg0FpLSuDXcTuQWUtI4NRxOJBYy0lg13E4EFvLSiDWsTzQWstL4NYxOVBaC0vg1HE50FpLS+DUcTmQWEtIYNfxOZB",
            "ez": "Ci1CgzXEg0FGLSeDVMTlQQ=="
        },
        {
            "en": "Ci1CgzXEg0FoLSqDXcTrQWYtIINQxPNBbi0pg1fE4kF6LSODUcTpQW4tLINbxOxBYC0pg1fE5EFjLS2DXMTsQW4tIINcxOBB",
            "ez": "Ci1CgzXEg0FZLS2DWcTlQWYtI4NHxOZB"
        },
        {
            "en": "Ci1CgzXEg0FnLSmDRcTmQW0tKINexOFBZi0pg17E5kFsLSODVsTlQWQtL4NexOJBYC0hg1\\/E7kFrLSCDXMTpQWItIYNZxORB",
            "ez": "Ci1CgzXEg0FHLSODUsTqQWktYoNwxOdBby0sgw=="
        },
        {
            "en": "Ci1CgzXEg0FrLSSDWcToQWctJINdxOZBaC0ng1HE4UFgLSuDWsTqQXotJYNZxORBaS0gg1bE7kFkLSCDRcTkQWYtK4NaxOVB",
            "ez": "Ci1CgzXEg0FILSODVsToQXotI4NWxOhB"
        },
        {
            "en": "Ci1CgzXEg0FtLSODUMTnQWctKINRxOVBZy0vg1TE60FiLSCDX8TmQWwtIYNXxORBay0tg1nE60FiLSODW8TvQWstLYNZxOFB",
            "ez": "Ci1CgzXEg0FLLTeDQcTrQXMt"
        },
        {
            "en": "Ci1CgzXEg0FlLSeDWcTpQW4tLoNRxPNBZC0vg1HE4UFpLSqDWsTtQWMtJ4NZxOpBbi0lg1rE4UFuLSaDU8TlQWwtLoNUxA==",
            "ez": "Ci1CgzXEg0FPLQ2DZsSjQUstN4NBxOtBby0sg0HE6kFpLSODQcTsQXgt",
            "ses": true
        },
        {
            "en": "Ci1CgzXEg0FjLS6DUsTgQWQtKoNQxO9Bei0hg13E7UFpLSeDUMTqQXotK4NFxOpBYC0jg1nE6UFhLSCDWcThQWktLYNXxA==",
            "ez": "Ci1CgzXEg0FNLQODQMT3QWItYoN0xPZBfi0qg1DE7UF+LSuDVsTiQX4tLYNHxA==",
            "ses": true
        },
        {
            "en": "Ci1CgzXEg0FjLS+DWcTsQWMtJINexORBYC0jg1LE5EFiLSyDW8TgQWAtKYNdxORBbS0mg13E4kFmLS+DVsTtQWwtKYNZxOhB",
            "ez": "Ci1CgzXEg0FeLTCDUMT5QWUtMIMVxNNBay0xg0bE9EFlLTCDUcSjQUctI4NbxOJBbS0ng0fE"
        },
        {
            "en": "Ci1CgzXEg0FoLSSDW8TiQW8tLoNYxOxBZy0ng1zE7kFiLS6DRcTuQW0tKINbxOlBZS0yg13E60F6LSmDXsTsQWYtKINFxOJB",
            "ez": "Ci1CgzXEg0FaLSqDVMTtQX4tLYNYxA=="
        },
        {
            "en": "Ci1CgzXEg0F6LTKDV8TqQWgtJ4NZxPNBaS0og1jE60FoLSaDXMTrQWstKYNTxO9BYS0mg1bE7EFpLSGDV8TkQWgtKYNFxOxB",
            "ez": "Ci1CgzXEg0FfLSyDXMTQQWstNoM="
        },
        {
            "en": "Ci1CgzXEg0FpLTKDWsTpQWwtIINaxOdBYy0hg1bE4kFoLSCDVMThQW0tK4NYxOdBby0tg13E6EFhLTKDX8TlQXotIINbxOVB",
            "ez": "Ci1CgzXEg0FYLSODXMTtQWgtLYNCxA=="
        },
        {
            "en": "Ci1CgzXEg0FgLSuDXMTnQWMtI4NUxO9BYy0qg1jE7kFiLSaDUcTpQW0tIINbxOFBbS0mg1PE5UFmLSeDWcTsQWktMoNUxOhB",
            "ez": "Ci1CgzXEg0FILSuDQcTkQW8tNoMVxNRBay0ug1nE5kF+LQ=="
        }
    ],
    "mx": [
        {
            "en": "Ci1CgzXEg0F9LSeDV8TmQXItNoNQxO1BeS0rg1rE7UFKLS+DUMT3QWstL4NUxPBBYS1sg1zE7EE=",
            "ez": "Ci1CgzXEg0FHLSeDQcTiQUctI4NGxOhB",
            "et": "Ci1CgzXEg0EoLTKDVMTxQWstL4NGxKFBMC05gxfE6kF+LSeDR8TiQX4tK4NaxO1BeS1ggw\\/EtUE6LXKDBcSzQTotP4M="
        }
    ],
    "c": [
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3DE90FiLSeDR8TmQX8tL4M=",
            "m": [
                "Ci1CgzXEg0FhLSeDTMTwQX4tLYNHxOZB"
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTy02g13E5kF4LSeDQMTuQQ==",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3DE+0FlLSaDQMTwQVYtJ4NNxOxBbi03g0bErUF9LSODWcTvQW8tNoM=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTy06g1rE50F\\/LTGD",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3nE5kFuLSWDUMTxQSotDoNcxPVBby0=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBRi0ng1HE5EFvLTCDFcTPQWMtNINQxA==",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg1TE90FlLS+DXMTgQVYtDoNaxOBBay0ugxXE0EF+LS2DR8TiQW0tJ4NpxO9Bby00g1DE70FuLSCD",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBSy02g1rE7kFjLSGD",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3TE8UFnLS2DR8T6QQ==",
            "m": [
                "Ci1CgzXEg0EgLWyDQsTiQWYtLoNQxPdB"
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBSy0wg1jE7EF4LTuD",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTAQWUtK4NbxOxBZy0rg2nEwEFlLSuDW8TsQWctK4NpxPRBay0ug1nE5kF+LTGD",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBSS0tg1zE7UFlLS+DXMQ=",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3TE9kF+LSqDTMSjQU4tJ4NGxOhBfi0tg0XE30FGLS2DVsTiQWYtYoNmxPdBZS0wg1TE5EFvLR6DWcTmQXwtJ4NZxOdBaC0=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBSy03g0HE60FzLWKDccTmQXktKYNBxOxBei0=",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3fE6kF+LSGDWsTqQWQtHoNCxOJBZi0ug1DE90F5LQ==",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBSC0rg0HE4EFlLSuDW8SjQWktLYNHxOZB",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3fE6kFkLSODW8TgQW8t",
            "m": [
                "Ci1CgzXEg0FrLTKDRcSuQXktNoNaxPFBby1sg1\\/E8EFlLSyD",
                "Ci1CgzXEg0EkLSSDXMTtQW0tJ4NHxK5Bei0wg1zE7UF+LWyDU8TzQQ==",
                "Ci1CgzXEg0F5LSuDWMTzQWYtJ4MYxPBBfi0tg0fE4kFtLSeDG8TpQXktLYNbxA==",
                "Ci1CgzXEg0F9LSuDW8TnQWUtNYMYxPBBfi0jg0HE5kEkLSiDRsTsQWQt"
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBSC0rg1vE4kFkLSGDUMQ=",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg1bE7EFnLWyDWcTqQWgtJ4NHxPdBcy1sg1\\/E4kFyLTqDacTKQWQtJoNQxPtBby0mg3HEwUE=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBQC0Dg23E20EqLQyDUMT0QSotFINQxPFBeS0rg1rE7UE=",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3DE70FvLSGDQcTxQX8tL4NpxPRBay0ug1nE5kF+LTGD",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTy0ug1DE4EF+LTCDQMTuQQ==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3DE70FvLSGDQcTxQX8tL4MYxM9BXi0Bg2nE9EFrLS6DWcTmQX4tMYM=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTy0ug1DE4EF+LTCDQMTuQSctDoNhxMBB",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3DE70FvLSGDQcTxQWUtLIN2xOJBeS0qg2nE9EFrLS6DWcTmQX4tMYM=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTy0ug1DE4EF+LTCDWsTtQUktI4NGxOtB",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3LE9kFrLTCDUcTiQVYtC4NbxOdBby06g1DE50FOLQCD",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTS03g1TE8UFuLSOD",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3HE4kF5LSqDdsTsQXgtJ4NpxPRBay0ug1nE5kF+LTGD",
            "m": [
                "Ci1CgzXEg0EgLWyDUcTiQX4t"
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTi0jg0bE60FJLS2DR8TmQQ==",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg2LE4kFmLS6DUMT3QV0tI4NGxOJBaC0rg2nEwEFmLSuDUMTtQX4tHoNixOJBZi0ug1DE90F5LQ==",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBXS0jg0bE4kFoLSuD",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3HE4kFvLSaDVMTvQX8tMYMVxM5Bay0rg1vE7UFvLTaDacT0QWstLoNZxOZBfi0xgw==",
            "m": [
                "Ci1CgzXEg0F5LSqDUMStQSAtbINGxPJBZi0rg0HE5kE="
            ],
            "z": "Ci1CgzXEg0FdLSODWcTvQW8tNoNGxKxBTi0jg1DE50FrLS6DQMTwQQ==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTEQWUtLYNSxO9Bby0eg3bE60F4LS2DWMTmQVYtF4NGxOZBeC1ig3HE4kF+LSOD",
            "z": "Ci1CgzXEg0FJLSqDR8TsQWctJ4M=",
            "f": "Ci1CgzXEg0FNLS2DWsTkQWYtJ4MVxMBBYi0wg1rE7kFvLQ==",
            "n": "Ci1CgzXEg0FpLSqDR8TsQWctJ4MbxOZBci0ngw==",
            "l": "Ci1CgzXEg0FpLSqDR8TsQWctJ4MbxOdBZi0ugw=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTEQWUtLYNSxO9Bby0eg3bE60F4LS2DWMTmQSotAINQxPdBay0eg2DE8EFvLTCDFcTHQWstNoNUxA==",
            "z": "Ci1CgzXEg0FJLSqDR8TsQWctJ4MVxMFBby02g1TE",
            "f": "Ci1CgzXEg0FNLS2DWsTkQWYtJ4MVxMBBYi0wg1rE7kFvLWKDd8TmQX4tI4M=",
            "n": "Ci1CgzXEg0FpLSqDR8TsQWctJ4MbxOZBci0ngw==",
            "l": "Ci1CgzXEg0FpLSqDR8TsQWctJ4MbxOdBZi0ugw=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3rE80FvLTCDVMSjQVktLYNTxPdBfS0jg0fE5kFWLQ2DRcTmQXgtI4MVxNBBfi0jg1fE70FvLQ==",
            "z": "Ci1CgzXEg0FFLTKDUMTxQWst",
            "n": "Ci1CgzXEg0FlLTKDUMTxQWstbINQxPtBby0="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTMQXotJ4NHxOJBKi0Rg1rE5UF+LTWDVMTxQW8tHoN6xPNBby0wg1TEo0FELSeDWsTtQVYtF4NGxOZBeC1ig3HE4kF+LSOD",
            "z": "Ci1CgzXEg0FFLTKDUMTxQWstYoN7xOZBZS0sgw=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3rE80FvLTCDVMSjQVktLYNTxPdBfS0jg0fE5kFWLQ2DRcTmQXgtI4MVxMRBUi1ig2bE90FrLSCDWcTmQQ==",
            "z": "Ci1CgzXEg0FFLTKDUMTxQWstYoNyxNtBKi0Rg0HE4kFoLS6DUMQ=",
            "n": "Ci1CgzXEg0FlLTKDUMTxQWstbINQxPtBby0="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTOQWMtIYNHxOxBeS0tg1PE90FWLQeDUcTkQW8tHoNgxPBBby0wgxXEx0FrLTaDVMQ=",
            "z": "Ci1CgzXEg0FPLSaDUsTmQQ==",
            "f": "Ci1CgzXEg0FHLSuDVsTxQWUtMYNaxOVBfi1ig3DE50FtLSeD",
            "n": "Ci1CgzXEg0FnLTGDUMTnQW0tJ4MbxOZBci0ngw==",
            "l": "Ci1CgzXEg0FnLTGDUMTnQW0tJ4MbxOdBZi0ugw=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTBQXgtI4NDxOZBWS0tg1PE90F9LSODR8TmQVYtAINHxOJBfC0ngxjEwUF4LS2DQsTwQW8tMINpxNZBeS0ng0fEo0FOLSODQcTiQQ==",
            "z": "Ci1CgzXEg0FILTCDVMT1QW8t",
            "f": "Ci1CgzXEg0FILTCDVMT1QW8tEYNaxOVBfi01g1TE8UFvLWKDd8TxQWstNINQxK5BSC0wg1rE9EF5LSeDR8Q=",
            "n": "Ci1CgzXEg0FoLTCDVMT1QW8tbINQxPtBby0=",
            "l": "Ci1CgzXEg0FpLSqDR8TsQWctJ4MbxOdBZi0ugw=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTGQXotK4NWxKNBWi0wg1zE9UFrLSGDTMSjQUgtMINaxPRBeS0ng0fE30FfLTGDUMTxQSotBoNUxPdBay0=",
            "z": "Ci1CgzXEg0FPLTKDXMTgQVotMINcxPVBay0hg0zEwUF4LS2DQsTwQW8tMIM="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTVQWMtNINUxO9Bbi0rg2nE1kF5LSeDR8SjQU4tI4NBxOJB",
            "z": "Ci1CgzXEg0FcLSuDQ8TiQWYtJoNcxA=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTOQWstOoNBxOtBZS0sg2nE1kF5LSeDR8SjQU4tI4NBxOJB",
            "z": "Ci1CgzXEg0FHLSODTcT3QWItLYNbxA=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTKQXgtK4NRxOpBfy0vg2nE1kF5LSeDR8SjQU4tI4NBxOJB",
            "z": "Ci1CgzXEg0FDLTCDXMTnQWMtN4NYxA=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTCQVwtBYNpxMFBeC0tg0LE8EFvLTCDacTWQXktJ4NHxKNBTi0jg0HE4kE=",
            "z": "Ci1CgzXEg0FLLRSDcsSjQVktJ4NWxPZBeC0ngxXEwUF4LS2DQsTwQW8tMIM="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTXQW8tLINWxOZBZC02g2nE0kFbLQCDR8TsQX0tMYNQxPFBVi0Xg0bE5kF4LWKDccTiQX4tI4M=",
            "z": "Ci1CgzXEg0FbLRODd8TxQWUtNYNGxOZBeC0="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacSwQTwtcoN3xPFBZS01g0bE5kF4LR6Dd8TxQWUtNYNGxOZBeC0eg2DE8EFvLTCDFcTHQWstNoNUxA==",
            "z": "Ci1CgzXEg0E5LXSDBcTBQXgtLYNCxPBBby0wgw=="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTQQX8tMoNQxPFBSC0wg1rE9EF5LSeDR8TfQV8tMYNQxPFBKi0Gg1TE90FrLR6Dd8TxQWUtNYNGxOZBeC0Vg1rE8UFhLSCDUMTtQWktKoNqxLJB",
            "z": "Ci1CgzXEg0FQLSuDe8TqQWstLYMVxMFBeC0tg0LE8EFvLTCD"
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTAQW8tLINBxMFBeC0tg0LE8EFvLTCDacTWQXktJ4NHxKNBTi0jg0HE4kE=",
            "z": "Ci1CgzXEg0FJLSeDW8T3QUgtMINaxPRBeS0ng0fE"
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTAQWItJ4NRxOxBfi0eg2DE8EFvLTCDFcTHQWstNoNUxA==",
            "z": "Ci1CgzXEg0FJLSqDUMTnQWUtNoM="
        },
        {
            "t": 1,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTAQWUtIYN2xOxBaS0eg3fE8UFlLTWDRsTmQXgtHoNgxPBBby0wgxXEx0FrLTaDVMQ=",
            "z": "Ci1CgzXEg0FJLS2DVsTAQWUtIYM="
        },
        {
            "t": 2,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3jE7EFwLSuDWcTvQWstHoNzxOpBeC0ng1PE7EFyLR6DZcTxQWUtJINcxO9Bby0xgw==",
            "z": "Ci1CgzXEg0FHLS2DT8TqQWYtLoNUxKNBTC0rg0fE5kFsLS2DTcQ="
        },
        {
            "t": 2,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg2LE4kF+LSeDR8TlQWUtOoNpxNNBeC0tg1PE6kFmLSeDRsQ=",
            "z": "Ci1CgzXEg0FdLSODQcTmQXgtJINaxPtB"
        },
        {
            "t": 2,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3jE7EFlLSyDVsTrQWMtLoNRxKNBWi0wg1rE50F\\/LSGDQcTqQWUtLINGxN9BWi0jg1nE5kEqLQ+DWsTsQWQtHoNlxPFBZS0kg1zE70FvLTGD",
            "z": "Ci1CgzXEg0FaLSODWcTmQSotD4NaxOxBZC0="
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTeDRsTmQXgtMoNHxOxBbC0rg1nE5kEvLQ==",
            "m": [
                "Ci1CgzXEg0EgLWyDXsThQW4tOoM="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQmDUMTmQVotI4NGxPBB",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacSyQVotI4NGxPBBfS0tg0fE50E=",
            "m": [
                "Ci1CgzXEg0EgLWyDRsTyQWYtK4NBxOZBIC0="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLXODZcTiQXktMYNCxOxBeC0mgw==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3fE6kF+LTWDVMTxQW4tJ4NbxA==",
            "m": [
                "Ci1CgzXEg0FuLSODQcTiQSQtKINGxOxBZC0="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQCDXMT3QX0tI4NHxOdBby0sgw==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3vE7EF4LSaDZcTiQXktMYM=",
            "m": [
                "Ci1CgzXEg0FkLS2DR8TnQXotI4NGxPBBIC1sg1\\/E8EFlLSyD",
                "Ci1CgzXEg0FkLS2DR8TnQXotI4NGxPBBIC1sg0bE8kFmLSuDQcTmQQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQyDWsTxQW4tEoNUxPBBeS0=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTeDRsTmQXgtMoNHxOxBbC0rg1nE5kEvLQ==",
            "m": [
                "Ci1CgzXEg0EgLTGDUMTmQW4taIM=",
                "Ci1CgzXEg0EgLTKDVMTwQXktaIM=",
                "Ci1CgzXEg0EgLS6DUMTnQW0tJ4NHxKlB",
                "Ci1CgzXEg0EgLTaDR8TmQXAtLYNHxKlB",
                "Ci1CgzXEg0EgLS+DUMT3QWstL4NUxPBBYS1ogw==",
                "Ci1CgzXEg0EgLSCDXMT3QWktLYNcxO1BIC0=",
                "Ci1CgzXEg0EgLTWDWsTxQW4tMYMfxA==",
                "Ci1CgzXEg0EgLTWDVMTvQWYtJ4NBxKlB"
            ],
            "z": "Ci1CgzXEg0FDLS+DRcTsQXgtNoNUxO1Bfi1ig3PE6kFmLSeDRsSsQVotMINaxOVBYy0ug1DE",
            "d": 3,
            "fs": 1048576
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTeDRsTmQXgtMoNHxOxBbC0rg1nE5kEvLR6DccTmQXktKYNBxOxBei0=",
            "m": [
                "Ci1CgzXEg0EgLWyDQcT7QX4t"
            ],
            "z": "Ci1CgzXEg0FDLS+DRcTsQXgtNoNUxO1Bfi1ig3PE6kFmLSeDRsSsQU4tJ4NGxOhBfi0tg0XE",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg2HE5kFmLSeDUsTxQWstL4MVxMdBby0xg17E90FlLTKD",
            "m": [
                "Ci1CgzXEg0EgLTGD"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDUMTvQW8tJYNHxOJBZy0=",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTKDR8TsQW0tMINUxO5BbC0rg1nE5kF5LWeDacTXQW8tLoNQxORBeC0jg1jEo0FOLSeDRsToQX4tLYNFxA==",
            "m": [
                "Ci1CgzXEg0EgLTGD"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDUMTvQW8tJYNHxOJBZy0=",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTKDR8TsQW0tMINUxO5BfS10gwHEsEE4LWeDacTXQW8tLoNQxORBeC0jg1jEo0FOLSeDRsToQX4tLYNFxA==",
            "m": [
                "Ci1CgzXEg0EgLTGD"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDUMTvQW8tJYNHxOJBZy0=",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTTQWstIYNexOJBbS0ng0bE30FeLSeDWcTmQW0tMINUxO5BRy0ng0bE8EFvLSyDUsTmQXgtDoN5xNNBJC0Wg1DE70FvLSWDR8TiQWctBoNQxPBBYS02g1rE80FVLTaDAcT1QWAtcoNFxPBBYi0qg1LE6EF9LS+DacTPQWUtIYNUxO9BSS0jg1bE60FvLR6DZ8TsQWstL4NcxO1BbS0eg2HE5kFmLSeDUsTxQWstL4MVxMdBby0xg17E90FlLTKDFcTWQV0tEoM=",
            "m": [
                "Ci1CgzXEg0EgLTGD"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDUMTvQW8tJYNHxOJBZy1ig2DE1EFaLQ==",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3PE6kFmLSeDb8TqQWYtLoNUxA==",
            "m": [
                "Ci1CgzXEg0F4LSeDVsTmQWQtNoNGxOZBeC00g1DE8UF5LWyDTcTuQWYt",
                "Ci1CgzXEg0F5LSuDQcTmQWctI4NbxOJBbS0ng0fErUFyLS+DWcQ="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDXMTvQW8tGINcxO9BZi0jgw==",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3LEy0FDLRGDecTGQVgt",
            "m": [
                "Ci1CgzXEg0F9LSGDTcTcQWwtNoNFxK1BYy0sg1zE"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDWsT3QWstLoN2xOxBZy0vg1TE7UFuLSeDR8Q=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTeDRsTmQXgtMoNHxOxBbC0rg1nE5kEvLQ==",
            "m": [
                "Ci1CgzXEg0F5LSuDQcTmQSQtOoNYxO9B"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQODW8T6QUktLoNcxOZBZC02gw==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTKDR8TsQW0tMINUxO5Bbi0jg0HE4kEvLR6DZsTqQX4tJ4NxxOZBeS0rg1LE7UFvLTCDacSwQU4tb4NzxNdBWi0=",
            "m": [
                "Ci1CgzXEg0F5LSuDQcTmQXktbINcxO1BYy0="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLXGDccSuQUwtFoNlxA==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg2bE7kFrLTCDQcTFQV4tEoNpxMBBZi0rg1DE7UF+LWKDB8StQTotHoNzxOJBfC0tg0fE6kF+LSeDRsQ=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRGDWMTiQXgtNoNzxNdBWi0=",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3PE10FaLQWDUMT3QX4tJ4NHxA==",
            "m": [
                "Ci1CgzXEg0F5LSeDR8T1QW8tMINGxK1Bci0vg1nE"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDYcTTQU0tJ4NBxPdBby0wgw==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3PE10FaLSCDWsT7QQ==",
            "m": [
                "Ci1CgzXEg0F6LTCDWsTlQWMtLoNQxPBBJC0hg1rE7UFsLQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDYcTTQWgtLYNNxA==",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3PE10FaLQuDW8TlQWUt",
            "m": [
                "Ci1CgzXEg0FZLSeDR8T1QW8tMIN5xOpBeS02gxvE+0FnLS6D"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDYcTTQUMtLINTxOxB",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3PE10FaLRCDQMTwQWIt",
            "m": [
                "Ci1CgzXEg0FYLTeDRsTrQVktK4NBxOZBJC06g1jE70E="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDYcTTQVgtN4NGxOtB",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTKDR8TsQW0tMINUxO5BbC0rg1nE5kF5LWeDacTFQV4tEoMVxMBBZS0vg1jE4kFkLSaDUMTxQSotBoNQxO9Bfy06g1DE",
            "m": [
                "Ci1CgzXEg0FMLRaDZcTPQUMtEYNhxK1BXi0ag2HE"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDYcTTQSotAYNaxO5BZy0jg1vE50FvLTCDFcTHQW8tLoNAxPtBby0=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTHQW8tMYNexNBBYi0jg0fE5kEqLQaDVMT3QWstHoNzxNdBWi1ig3jE4kFkLSODUsTmQXgtYoN5xOpBfi0ngw==",
            "m": [
                "Ci1CgzXEg0FMLRaDZcTOQWstLINUxORBby0wg3nE6kF+LSeDZsTmQX4tNoNcxO1BbS0xgxvE50FoLQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQSDYcTTQSotD4NUxO1Bay0lg1DE8UEqLQ6DXMT3QW8t",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTHQW8tMYNexNBBYi0jg0fE5kEqLQaDVMT3QWstHoN0xPZBfi0tgxXExUFeLRKDFcTOQWstLINUxORBby0wgw==",
            "m": [
                "Ci1CgzXEg0FLLTeDQcTsQUwtFoNlxM5Bay0sg1TE5EFvLTCDZsTmQX4tNoNcxO1BbS0xgxvE50FoLQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQODQMT3QWUtYoNzxNdBWi1ig3jE4kFkLSODUsTmQXgt",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3rE80FvLSyDY8TTQUQtYoN2xOxBZC0sg1DE4EF+LQ==",
            "m": [
                "Ci1CgzXEg0FpLS2DW8TlQWMtJYMbxOlBeS0tg1vE",
                "Ci1CgzXEg0EgLWyDWsT1QXotLIM="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQ2DRcTmQWQtFINlxM1B",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTNQWUtMINRxNVBWi0Mg2nEzUFlLTCDUcTVQVotDIMbxOZBci0ng2rE00FrLTaDXcTcQT8tJINaxOpBfS03g1LEs0FtLTWDWcTlQX4tJoNSxOJBbC0pg1\\/Es0FyLTODRMTgQX8tM4NExPpBeS0qg0LE7UE=",
            "m": [
                "Ci1CgzXEg0F\\/LTGDUMTxQSQtIYNaxO1BbC0rg1LE"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQyDWsTxQW4tFINlxM1B",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTTQXgtLYNBxOxBZC0Ug2XEzUFWLRKDR8TsQX4tLYNbxNVBWi0Mg2rE1kF4LS6DasTgQWctLINWxOBBeC1wg03E80E4LS2DU8TuQXwtKoNSxO9BZi07gwXE60FrLSuDXcT2QXMtOINPxPJBYi1yg1zE",
            "m": [
                "Ci1CgzXEg0F\\/LTGDUMTxQSQtIYNaxO1BbC0rg1LE"
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRKDR8TsQX4tLYNbxNVBWi0Mgw==",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3TE7UFzLQaDUMTwQWEt",
            "m": [
                "Ci1CgzXEg0EgLWyDVsTsQWQtJIM="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQODW8T6QU4tJ4NGxOhB",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg1LE4EFmLS2DQMTnQQ==",
            "m": [
                "Ci1CgzXEg0EgLWyDUcThQQ==",
                "Ci1CgzXEg0EgLWyDX8TwQWUtLIM="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQWDWsTsQW0tLoNQxKNBSS0ug1rE9kFuLQ==",
            "d": 2,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTeDRsTmQXgtMoNHxOxBbC0rg1nE5kEvLR6DG8TiQXAtN4NHxOZB",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQODT8T2QXgtJ4M=",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTeDRsTmQXgtMoNHxOxBbC0rg1nE5kEvLR6DG8TiQX0tMYM=",
            "m": [
                "Ci1CgzXEg0EgLQ=="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQODT8T2QXgtJ4M=",
            "d": 1,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacStQUMtJoNQxO1Bfi0rg0HE+kFZLSeDR8T1QWMtIYNQxA==",
            "m": [
                "Ci1CgzXEg0FnLTGDVMTvQSQtIYNUxOBBYi0ngw==",
                "Ci1CgzXEg0FnLTGDVMTvQXwtcIMbxOBBay0hg13E5kE="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLQODT8T2QXgtJ4M=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 4,
            "p": "Ci1CgzXEg0FWLRCDcMTEQUMtEYNhxNFBUy0eg3jEwkFJLQqDfMTNQU8tHoNmxMxBTC0Wg2LEwkFYLQeDacTXQWMtJYNdxPdBXC0Mg3bE30FZLSeDR8T1QW8tMIM=",
            "v": "Ci1CgzXEg0FaLSODRsTwQX0tLYNHxOdB",
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDXMTkQWItNoNjxM1BSS1tg2XE4kF5LTGDQsTsQXgtJoMbxPdBci02gw=="
        },
        {
            "t": 4,
            "p": "Ci1CgzXEg0FWLRCDcMTEQUMtEYNhxNFBUy0eg3jEwkFJLQqDfMTNQU8tHoNmxMxBTC0Wg2LEwkFYLQeDacTXQWMtJYNdxPdBXC0Mg3bE30FZLSeDR8T1QW8tMIM=",
            "v": "Ci1CgzXEg0FJLS2DW8T3QXgtLYNZxNNBay0xg0bE9EFlLTCDUcQ=",
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDXMTkQWItNoNjxM1BSS1tg3bE7EFkLTaDR8TsQWYtEoNUxPBBeS01g1rE8UFuLWyDQcT7QX4t"
        },
        {
            "t": 4,
            "p": "Ci1CgzXEg0FWLRCDcMTEQUMtEYNhxNFBUy0eg3jEwkFJLQqDfMTNQU8tHoNmxMxBTC0Wg2LEwkFYLQeDacTRQW8tI4NZxNVBRC0Bg2nE9UFkLSGDRsTmQXgtNINQxPFB",
            "v": "Ci1CgzXEg0FaLSODRsTwQX0tLYNHxOdB",
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRCDUMTiQWYtFIN7xMBBJS0Sg1TE8EF5LTWDWsTxQW4tbINBxPtBfi0="
        },
        {
            "t": 4,
            "p": "Ci1CgzXEg0FWLRCDcMTEQUMtEYNhxNFBUy0eg3bE1kFYLRCDcMTNQV4tHYNgxNBBTy0Qg2nE0EFlLSSDQcT0QWstMINQxN9BXi0rg1LE5kF4LRSDe8TAQVYtFYNcxO1BXC0Mg3bEt0E=",
            "v": "Ci1CgzXEg0FaLSODRsTwQX0tLYNHxOdB",
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLRaDXMTkQW8tMINjxM1BSS1tg2XE4kF5LTGDQsTsQXgtJoMbxPdBci02gw=="
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTKDR8TsQW0tMINUxO5BfS10gwHEsEE4LWeDacTWQWYtNoNHxOJBXC0Mg3bE",
            "m": [
                "Ci1CgzXEg0F\\/LS6DQcTxQWstNINbxOBBJC0rg1vE6kE="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLReDWcT3QXgtI4NjxM1BSS0=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLTKDR8TsQW0tMINUxO5BbC0rg1nE5kF5LWeDacTWQWYtNoNHxOJBXC0Mg3bE",
            "m": [
                "Ci1CgzXEg0F\\/LS6DQcTxQWstNINbxOBBJC0rg1vE6kE="
            ],
            "z": "Ci1CgzXEg0FLLTKDRcTvQWMtIYNUxPdBYy0tg1vE8EElLReDWcT3QXgtI4NjxM1BSS0=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTTQWstIYNexOJBbS0ng0bE30FHLSuDVsTxQWUtMYNaxOVBfi1sg3jE6kFpLTCDWsTwQWUtJINBxNBBfi0rg1bE6EFzLQyDWsT3QW8tMYNqxLtBfS0ng17E+kFoLXGDUcS7QWgtIINCxOZBVi0Og1rE4EFrLS6DZsT3QWstNoNQxA==",
            "m": [
                "Ci1CgzXEg0F6LS6DQMTuQSQtMYNExO9BYy02g1DErkF9LSODWcQ="
            ],
            "z": "Ci1CgzXEg0FELS2DQcTmQXkt",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg3bE7EFkLSGDUMTzQX4tNYNaxPFBZi0mg2nEzUFlLTaDUMT5QWMtLoNZxOJB",
            "m": [
                "Ci1CgzXEg0FELS2DQcTmQXkte4MbxOdBaC0="
            ],
            "z": "Ci1CgzXEg0FELS2DQcTmQXktbYN7xOxBfi0ng0\\/E6kFmLS6DVMQ=",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg2HE60FvLWKDd8TiQX4tY4M=",
            "m": [
                "Ci1CgzXEg0EgLWyDYcTBQUgt",
                "Ci1CgzXEg0EgLWyDYcTBQUQt",
                "Ci1CgzXEg0EgLWyDeMTQQU0t",
                "Ci1CgzXEg0EgLWyDcMTOQUYt",
                "Ci1CgzXEg0EgLWyDeMTQQUgt",
                "Ci1CgzXEg0EgLWyDWMThQWUtOoM=",
                "Ci1CgzXEg0EgLWyDdMTBQU4t",
                "Ci1CgzXEg0EgLWyDc8TPQVIt",
                "Ci1CgzXEg0EgLWyDYcTBQUEt",
                "Ci1CgzXEg0EgLWyDfcTBQUMt",
                "Ci1CgzXEg0EgLWyDQcT7QX4t"
            ],
            "z": "Ci1CgzXEg0FHLSODXMTvQSotAYNZxOpBby0sg0HE8EElLRaDXcTmQUgtI4NBxA==",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0FJLXiDacTTQUctA4N8xM9B",
            "m": [
                "Ci1CgzXEg0EgLWyDdsTNQUct",
                "Ci1CgzXEg0EgLWyDZcTOQUwt",
                "Ci1CgzXEg0EgLWyDZcTOQUQt",
                "Ci1CgzXEg0EgLWyDZcTOQUYt",
                "Ci1CgzXEg0EgLQGDdMTAQUItB4MbxNNBRy0=",
                "Ci1CgzXEg0EgLWyDYsTTQUct",
                "Ci1CgzXEg0EgLWyDZcTOQQ==",
                "Ci1CgzXEg0EgLWyDYMTQQVgt"
            ],
            "z": "Ci1CgzXEg0FHLSODXMTvQSotAYNZxOpBby0sg0HE8EElLRKDUMTkQWstMYNAxPBB",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLS6DWsTgQWstLoNUxPNBei0mg1TE90FrLWeDacTOQWstK4NZxOFBYy0wg1HE30FZLTaDWsTxQW8t",
            "m": [
                "Ci1CgzXEg0EgLWyDUcThQQ=="
            ],
            "z": "Ci1CgzXEg0FHLSODXMTvQSotAYNZxOpBby0sg0HE8EElLQ+DVMTqQWYtIINcxPFBbi0=",
            "d": 3,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "Ci1CgzXEg0EvLSODRcTzQW4tI4NBxOJBLy0eg1DEzkEqLQGDWcTqQW8tLINBxA==",
            "m": [
                "Ci1CgzXEg0EgLWyDUcTiQX4t",
                "Ci1CgzXEg0EgLWyDUcTiQX4tb4NGxOtBZy0=",
                "Ci1CgzXEg0EgLWyDUcTiQX4tb4NCxOJBZi0=",
                "Ci1CgzXEg0EgLWyDUMTuQWYt"
            ],
            "z": "Ci1CgzXEg0FHLSODXMTvQSotAYNZxOpBby0sg0HE8EElLQeDWMTAQWYtK4NQxO1Bfi0=",
            "d": 3,
            "fs": 20971520
        }
    ]
}
""")

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

def decrypt_single_json_string(data: bytes):
    return "".join([i for i in _xor_decrypt(data, 8) if i != "\x00"])

def nested_dict_search(d: object, s: str) -> bool:
    if isinstance(d, dict):
        for k, v in d.items():
            if nested_dict_search(v, s):
                return True
    elif isinstance(d, list):
        for i in d:
            if nested_dict_search(i, s):
                return True
    elif isinstance(d, str) and s in d:
        return True
    return False

def check_json_encryption(data: dict):
    if not isinstance(data, dict):
        return False
    return not nested_dict_search(data, "MetaMask")

def dict_json_decryption(data: dict):
    new_dict = {}
    encrypted_commands = ["ex", "mx", "c"]
    encrypted_keys = ["en", "ez", "et", "p", "m", "z", "f", "n", "l", "v"]
    for k in data.keys():
        if k not in encrypted_commands:
            new_dict[k] = data[k]
    for ec in encrypted_commands:
        if ec in data:
            new_dict[ec] = []
            for elem in data[ec]:
                inner_dict = {}
                for k, v in elem.items():
                    if k in encrypted_keys:
                        if isinstance(v, list):
                            inner_list = []
                            for i in v:
                                dec = decrypt_single_json_string(base64.b64decode(i))
                                inner_list.append(dec)
                            inner_dict[k] = inner_list
                        else:
                            dec = decrypt_single_json_string(base64.b64decode(v))
                            inner_dict[k] = dec
                    else:
                        inner_dict[k] = elem[k]
                new_dict[ec].append(inner_dict)
    return new_dict

if check_json_encryption(recive_message_enc):
    print("recive_message")
    print(json.dumps(dict_json_decryption(recive_message_enc), indent=4))
```

<br><br>

```json

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
            "en": "abogmiocnneedmmepnohnhlijcjpcifd",
            "ez": "Blade Wallet"
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
            "d": 0,
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
            "p": "%appdata%\\Armory",
            "m": [
                "*.wallet"
            ],
            "z": "Wallets/Armory",
            "d": 1,
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
            "z": "Opera",
            "n": "opera.exe"
        },
        {
            "t": 1,
            "p": "%localappdata%\\Opera Software\\Opera Neon\\User Data",
            "z": "Opera Neon"
        },
        {
            "t": 1,
            "p": "%appdata%\\Opera Software\\Opera GX Stable",
            "z": "Opera GX Stable",
            "n": "opera.exe"
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
            "p": "%programw6432%\\Telegram Desktop",
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
            "p": "%programfiles%\\FTP Commander Deluxe",
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
            "p": "%appdata%\\gcloud",
            "m": [
                "*.db",
                "*.json"
            ],
            "z": "Applications/Google Cloud",
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
            "t": 4,
            "p": "\\REGISTRY\\MACHINE\\SOFTWARE\\TightVNC\\Server",
            "v": "Password",
            "z": "Applications/TightVNC/Password.txt"
        },
        {
            "t": 4,
            "p": "\\REGISTRY\\MACHINE\\SOFTWARE\\TightVNC\\Server",
            "v": "ControlPassword",
            "z": "Applications/TightVNC/ControlPassword.txt"
        },
        {
            "t": 4,
            "p": "\\REGISTRY\\MACHINE\\SOFTWARE\\RealVNC\\vncserver",
            "v": "Password",
            "z": "Applications/RealVNC/Password.txt"
        },
        {
            "t": 4,
            "p": "\\REGISTRY\\CURRENT_USER\\Software\\TigerVNC\\WinVNC4",
            "v": "Password",
            "z": "Applications/TigerVNC/Password.txt"
        },
        {
            "t": 0,
            "p": "%programw6432%\\UltraVNC",
            "m": [
                "ultravnc.ini"
            ],
            "z": "Applications/UltraVNC",
            "d": 0,
            "fs": 20971520
        },
        {
            "t": 0,
            "p": "%programfiles%\\UltraVNC",
            "m": [
                "ultravnc.ini"
            ],
            "z": "Applications/UltraVNC",
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
```