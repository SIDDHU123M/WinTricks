# Deep Windows 11 Secrets

These are **deep, advanced-level Windows 11 secrets** that even most power users don’t know. Much more **elite, under-the-hood list** with hidden settings, undocumented features, dev/debugging tools, and performance or hacking-level tricks:

***

### **Deep Windows 11 Secrets, Developer/Power Tricks**

#### 1. **Hidden Developer Settings in Taskbar**

*   Registry path:

    ```
    HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    ```
* Create `TaskbarSi` (DWORD):
  * `0` = small, `1` = medium, `2` = large icons.
* Create `Start_ShowClassicMode` (DWORD):
  * Set to `1` to restore classic Start Menu (Win10-like) — **only works on some builds**.

***

#### 2. **Shell Commands List (Hidden Explorer Locations)**

* Try in Run (`Win + R`) or address bar:
  * `shell:AppsFolder` – all apps installed (including hidden system apps)
  * `shell:Startup` – user startup folder
  * `shell:CommonStartup` – all users' startup
  * `shell:Recent` – list of recent files
  * `shell:SendTo` – customize "Send to" menu

***

#### 3. **Registry Hack – Disable Modern Context Menu**

*   Brings back old right-click menu:

    ```
    [HKEY_CURRENT_USER\Software\Classes\CLSID\
    {86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32]
    ```

    * Create new key above, leave `(Default)` empty.
    * Restart Explorer (or reboot).

***

#### 4. **Virtual Desktops with Independent Wallpapers**

* Each virtual desktop can have its own background.
  * Right-click the desktop thumbnail in `Task View`, choose `Choose background`.

***

#### 5. **Enable Hidden "Efficiency Mode" (Eco Mode) in Task Manager**

* Right-click a process > **Efficiency Mode**
  * Lowers process priority + throttles background CPU.

***

#### 6. **Boot to UEFI (No Reboot)**

*   Run:

    ```
    shutdown /r /fw /t 0
    ```
* Directly reboots into UEFI/BIOS — extremely useful for overclockers/tuners.

***

#### 7. **Enable Windows Package Manager (winget)**

*   Use `winget` (CLI package manager like apt/homebrew):

    ```
    winget install <app>
    winget upgrade --all
    ```
* Hidden commands:
  * `winget features` – toggles experimental features
  * `winget validate` – checks manifest structure

***

#### 8. **Turn On Hidden Diagnostic Mode**

*   Run:

    ```
    msconfig
    ```
* Boot tab > Select **Diagnostic startup**
  * Loads only essential services — great for debugging malware or system issues.

***

#### 9. **Disable Windows Defender Real-Time (via PowerShell)**

*   Use with caution:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring $true
    ```
*   Re-enable:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring $false
    ```

***

#### 10. **Force Enable Legacy Photo Viewer**

*   Registry path:

    ```
    Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Photo Viewer\Capabilities\FileAssociations
    ```
* Add string entries like `.jpg` = `PhotoViewer.FileAssoc.Tiff`
* Then "Open with" > "Windows Photo Viewer"

***

#### 11. **Real Admin Mode Shortcut (No UAC prompt)**

*   Create shortcut with:

    ```
    runas /user:Administrator "cmd.exe"
    ```
* If you enable the built-in Admin account (`net user administrator /active:yes`), this gives full access with no prompt.

***

#### 12. **Hidden Windows Event Log for Shutdown Reason**

* Event Viewer > Windows Logs > System
  *   Filter for:

      ```
      Event ID 1074
      ```

      * Shows who/what triggered shutdown or restart (great for debugging random reboots).

***

#### 13. **Bypass TPM 2.0 Check for Install**

*   In install media, open regedit:

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig
    ```

    * Create:
      * `BypassTPMCheck`=dword:00000001
      * `BypassSecureBootCheck`=dword:00000001
      * `BypassRAMCheck`=dword:00000001

***

#### 14. **Hyper Secret Folder Lock with CLSID Trick**

*   Create folder:

    ```
    YourFolderName.{2559a1f2-21d7-11d4-bdaf-00c04f60b9f0}
    ```
* It turns into a shortcut and becomes unopenable normally.

***

#### 15. **Create Undeletable/Unrenameable Folder (CMD Trick)**

*   Run CMD as admin:

    ```
    md "\\.\C:\con"
    ```
*   This uses a reserved name (`con`, `prn`, `nul`, etc.) — becomes undeletable via Explorer. Delete with:

    ```
    rmdir "\\.\C:\con"
    ```

***

#### 16. **Enable Hidden “Do Not Disturb” API (Auto Quiet Hours)**

*   Registry:

    ```
    HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Notifications\Settings
    ```

    * Tweak:
      * `NOC_GLOBAL_SETTING_TOASTS_ENABLED` = `0` (turns off all notifications)

***

#### 17. **Hidden "Boot Menu" on Startup**

* On boot, press:
  * `Shift + F8` (on some systems)
  * or hold **Shift** while clicking **Restart**
* Opens advanced boot options: Safe Mode, Debug, Recovery Shell.

***

#### 18. **NTFS Alternate Data Streams (ADS)**

*   Hide secret data in files:

    ```
    echo "Secret" > normal.txt:hidden.txt
    ```
* `normal.txt` looks unchanged — data is stored in a hidden stream.
*   Read it:

    ```
    more < normal.txt:hidden.txt
    ```

***

#### 19. **WMIC Legacy Control (Still Works!)**

*   Example: list BIOS info:

    ```
    wmic bios get serialnumber
    ```
*   List installed apps:

    ```
    wmic product get name
    ```

***

#### 20. **Disable Cortana Fully (Group Policy / Registry)**

*   Registry:

    ```
    HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search
    ```

    * Add DWORD: `AllowCortana` = `0`

***

Want me to send you **automation scripts, group policy templates, deep registry packs**, or a **script pack with all these secrets applied in one go**?
