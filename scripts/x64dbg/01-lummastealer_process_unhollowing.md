# LummaStealer process un-hollowing

```c
// clear breakpoints
bc

// defeats IsDebuggerPresent and manual PEB check
$peb = peb()
log "PEB beingdebugged flag at startup: {mem;1@$peb+0x2}"
set $peb+0x2, #00#
log "PEB beingdebugged flag forced to be 0: {mem;1@$peb+0x2}"

// try to dump process hollowing injection
created_process_handle = 0
created_process_id = 0
created_thread_id = 0

bp CreateProcessW
SetBreakpointCommand CreateProcessW, "scriptcmd call proccreate"

bp ReadProcessMemory
SetBreakpointCommand ReadProcessMemory, "scriptcmd call virtmemread"

bp WriteProcessMemory
SetBreakpointCommand WriteProcessMemory, "scriptcmd call virtmemwrite"

bp VirtualAllocEx
SetBreakpointCommand VirtualAllocEx, "scriptcmd call virtmemallocex"

bp VirtualAlloc
SetBreakpointCommand VirtualAlloc, "scriptcmd call virtmemalloc"

bp ResumeThread
SetBreakpointCommand ResumeThread, "scriptcmd call attachanddump"

goto main

proccreate:
    set procinfo, arg.get(9)
    rtr // run until return
    set created_process_handle, dword(procinfo)
    set created_process_id, dword(procinfo+8)
    set created_thread_handle, dword(procinfo+4)
    set created_thread_id, dword(procinfo+c)
    log "ProcessCreation -> PHandle: {x:created_process_handle}; THandle: {x:created_thread_handle}; PID: {u:created_process_id}, TID: {u:created_thread_id}"
    goto main

virtmemalloc:
    set base_addr, arg.get(0)
    set base_size, arg.get(1)
    log "VirtualAlloc -> base address: {x:arg.get(0)}, dwsize: {x:arg.get(1)}, alloc type: {x:arg.get(2)}, fl protect: {x:arg.get(3)}"
    rtr
    log "Ret value: {x:eax}"
    goto main

virtmemallocex:
    set base_addr, arg.get(1)
    set base_size, arg.get(2)
    log "VirtualAllocEx -> base address: {x:arg.get(1)} of process handle {x:arg.get(0)}, dwsize: {x:arg.get(2)}, alloc type: {x:arg.get(3)}, fl protect: {x:arg.get(4)}"
    rtr
    log "Ret value: {x:eax}"
    goto main

virtmemread:
    log "ProcessMemRead -> phandle {x:arg.get(0)}, memory address {x:arg.get(2)}[{x:arg.get(3)}]"
    rtr // run until return
    log "Read data: {mem;arg.get(3)@arg.get(2)}"
    goto main

virtmemwrite:
    set write_process, arg.get(0) // hProcess
    set buffer, arg.get(2) // lpBuffer
    rtr // run until return
    log "ProcessMemWrite -> phandle {x:write_process}, memory address {x:arg.get(1)}[{x:arg.get(3)}]"
    cmp word(buffer), 5a4d // compare the first 2 bytes at mem_addr address with "MZ"
    jne check_same_process
    log "Bytes starts with magic number MZ!"
    set created_process_handle, write_process
    goto main
    
// consider also new writes to this process
check_same_process:
    cmp write_process, created_process_handle
    jne main
    log "Another write to the same process..."
    goto main

attachanddump:
    log "Resume THandle: {x:arg.get(0)}"
    set thandle, arg.get(0) // hThread
    cmp thandle, created_thread_handle
    jne main
    log "Stored THandle: {u:created_thread_handle}; Resumed THandle: {u:thandle}"
    attach created_process_id
    log "Run this command in the command-line: savedata :memdump:, base_addr, base_size"
    pause
    
main:
    run

ret
```

<br><br>

<p><img src="{{ site.url }}{{ site.baseurl }}/scripts/x64dbg/01-lummastealer_process_no_hollowing.png" alt="lummastealer process no-hollowing output" width="100%"/></p>