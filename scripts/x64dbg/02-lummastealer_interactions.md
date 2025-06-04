# LummaStealer interactions

```c
// clear breakpoints
bc

// Disable debugger checks
$peb = peb()
log "PEB beingdebugged flag at startup: {mem;1@$peb+0x2}"
set $peb+0x2, #00#
log "PEB beingdebugged flag forced to be 0: {mem;1@$peb+0x2}"

// Set LoadLibraryExW to hook DLLs
bp LoadLibraryExW
SetBreakpointCommand LoadLibraryExW, "scriptcmd call checkdlls"

goto main

checkdlls:
    log "DLL NAME: {utf16(arg.get(0))}"
    is_winhttp = streq(utf16(arg.get(0)), "winhttp.dll")
    cmp is_winhttp, 1
    jne main
    rtr
    bp WinHttpOpen
    SetBreakpointCommand WinHttpOpen, "scriptcmd call winhttpopen"
    bp WinHttpConnect
    SetBreakpointCommand WinHttpConnect, "scriptcmd call winhttpconnect"
    bp WinHttpOpenRequest
    SetBreakpointCommand WinHttpOpenRequest, "scriptcmd call winhttpopenrequest"
    bp WinHttpSendRequest
    SetBreakpointCommand WinHttpSendRequest, "scriptcmd call winhttpsendrequest"
    bp WinHttpReceiveResponse
    SetBreakpointCommand WinHttpReceiveResponse, "scriptcmd call winhttpreceiveresponse"
    goto main

winhttpopen:
    log "WinHttpOpen called"
    goto main

winhttpconnect:
    log "WinHttpConnect to: {utf16(arg.get(1))}:{d:arg.get(2)}"
    goto main

winhttpopenrequest:
    log "WinHttpOpenRequest: Method={utf16(arg.get(1))}, URI={utf16(arg.get(2))}"
    goto main

winhttpsendrequest:
    log "WinHttpSendRequest: Headers={utf16(arg.get(1))}, Data={s:arg.get(3)}"
    goto main

winhttpreceiveresponse:
    log "WinHttpReceiveResponse called"
    goto main

main:
    run
```

<br><br>

<p><img src="{{ site.url }}{{ site.baseurl }}/scripts/x64dbg/02-lummastealer_interactions.png" alt="lummastealer interactions output" width="100%"/></p>