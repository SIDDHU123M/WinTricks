# Ultimate Windows 11 Registry Hacks

Registry-level sorcery — where Windows keeps all its **deepest dark secrets**. Below are **Registry tweaks** that unlock powerful features, hidden UI options, performance upgrades, security bypasses, and more. **Make a backup before modifying!**&#x20;

***

> ⚠️ **Disclaimer:**\
> Not all tweaks and registry edits work on every device or Windows 11 build. Some features may depend on your hardware (e.g., touchpad support, battery settings), specific OEM restrictions, or group policy settings in place.\
> Always **create a system restore point** or back up your registry before making changes. Test carefully and proceed at your own risk.

***

#### **A. Backup the Entire Registry (Recommended Before Tweaks)**

**Method 1: Create a `.reg` file to export current registry (manual)**

Create a `.bat` file with the following content:

```bat
@echo off
setlocal
set TIMESTAMP=%DATE:/=-%_%TIME::=-%
set TIMESTAMP=%TIMESTAMP: =%
reg export HKLM\ "FullRegistryBackup_HKLM_%TIMESTAMP%.reg" /y
reg export HKCU\ "FullRegistryBackup_HKCU_%TIMESTAMP%.reg" /y
echo Registry backup complete.
pause
```

> This will create two files:
>
> * `FullRegistryBackup_HKLM_*.reg`
> * `FullRegistryBackup_HKCU_*.reg`

***

#### **B. Restore the Registry**

If anything breaks, simply double-click the corresponding `.reg` backup file you exported above, or run:

```bat
reg import FullRegistryBackup_HKLM_*.reg
reg import FullRegistryBackup_HKCU_*.reg
```

> ⚠️ You must run this as **Administrator** to restore system-level (HKLM) changes.

***

#### Optional: System Restore Point (Safer)

If you'd prefer to create a full system restore point:

Create a `.ps1` (PowerShell) script:

```powershell
Checkpoint-Computer -Description "BeforeWindowsTweaks" -RestorePointType "MODIFY_SETTINGS"
```

Then run PowerShell **as administrator**, and execute the script above.

***

## Ultimate Windows 11 Registry Hacks

#### Location: All registry tweaks below are located using:

```
Win + R → regedit
```

***

#### 1. **Enable Ultimate Performance Mode**

* **Path:**\
  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power`
* **Add Key:** `PowerThrottling` → New DWORD `PowerThrottlingOff = 1`
*   Then in Terminal:

    ```bash
    powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
    ```
* Use it via Control Panel > Power Options.

***

#### 2. **Speed Up Right-Click Context Menu**

* **Path:**\
  `HKEY_CLASSES_ROOT\*\shellex\ContextMenuHandlers`
* Delete unnecessary handlers (e.g., OneDrive, NVIDIA, WinRAR if you don’t use them)
* Speeds up right-click instantly.

***

#### 3. **Unlock “God Mode” Panel**

*   Make a folder named:

    ```
    GodMode.{ED7BA470-8E54-465E-825C-99712043E01C}
    ```
* Gives you a **master control panel** with every setting in one place.

***

#### 4. **Add “Open With Notepad” to All Files**

* **Path:**\
  `HKEY_CLASSES_ROOT\*\shell\Open with Notepad`
* Create key → inside it add:
  *   `command` key:

      ```
      notepad.exe %1
      ```

***

#### 5. **Enable Classic File Explorer Ribbon**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions\Blocked`
*   Add new **String value**:

    ```
    {e2bf9676-5f8f-435c-97eb-11607a5bedf7}
    ```

***

#### 6. **Disable Windows Defender Permanently**

> (For dev/test boxes only — not recommended on live systems)

* **Path:**\
  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender`
* Create `DWORD: DisableAntiSpyware = 1`

***

#### 7. **Show Seconds on Taskbar Clock**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
* Add `DWORD: ShowSecondsInSystemClock = 1`

***

#### 8. **Disable Windows Update Completely**

* **Path:**\
  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU`
* Add `DWORD: NoAutoUpdate = 1`

***

#### 9. **Disable Lock Screen (Boot Straight to Desktop)**

* **Path:**\
  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Personalization`
* Add `DWORD: NoLockScreen = 1`

***

#### 10. **Add “Take Ownership” to Right-Click**

*   **Path:**\
    Create `.reg` file with:

    ```reg
    Windows Registry Editor Version 5.00

    [HKEY_CLASSES_ROOT\*\shell\runas]
    @="Take Ownership"
    "NoWorkingDirectory"=""

    [HKEY_CLASSES_ROOT\*\shell\runas\command]
    @="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F"
    ```

***

#### 11. **Hide Drives in Explorer**

* **Path:**\
  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer`
* Add `DWORD: NoDrives`
* Value:
  * A = A: drive = 1
  * B = 2
  * C = 4
  * D = 8 ...
  * To hide C and D → 4 + 8 = `12`

***

#### 12. **Customize OEM Info in System Properties**

* **Path:**\
  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\OEMInformation`
* Add strings like:
  * `Manufacturer`, `Model`, `SupportURL`, `Logo` (path to BMP)

***

#### 13. **Custom Boot Logo / Boot Text**

> Requires modifying:

* `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\BootControl`
* Or use tools like **HackBGRT** (careful — low-level boot stuff)

***

#### 14. **Force Taskbar to Top / Left / Right**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\StuckRects3`
* Modify the fifth row’s 13th byte (TaskbarPosition):
  * 00 = bottom
  * 01 = left
  * 02 = right
  * 03 = top
* Reboot Explorer (`taskkill /f /im explorer.exe` → restart)

***

#### 15. **Enable Clipboard History and Sync**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Microsoft\Clipboard`
* Add `DWORD: EnableClipboardHistory = 1`
* Add `DWORD: EnableCloudClipboard = 1`

***

#### 16. **Hide Specific Control Panel Items**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`
*   Add:

    ```
    DWORD: DisallowCpl = 1
    Key: DisallowCpl → New String: 1 = appwiz.cpl (example)
    ```
* Hide stuff like `appwiz.cpl`, `inetcpl.cpl`, etc.

***

#### 17. **Disable “Shortcut” Suffix in New Shortcuts**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer`
*   Add:

    ```
    DWORD: Link = 0
    ```
* Removes `- Shortcut` from shortcut names.

***

#### 18. **Disable Windows 11 Snap Layouts Hover**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
*   Add:

    ```
    DWORD: DisableSnapAssistFlyout = 1
    ```

***

#### 19. **Disable “Suggested” Apps in Start Menu**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager`
*   Set the following DWORDs to `0`:

    ```
    SubscribedContent-338389Enabled
    SubscribedContent-353694Enabled
    SubscribedContent-353696Enabled
    ```

***

#### 20. **Set Custom Folder for File Explorer Default Launch**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
*   Modify:

    ```
    DWORD: LaunchTo = 1
    ```
* Values:
  * `1` = Quick access
  * `2` = This PC
  * `3` = Home

***

#### 21. **Restrict Task Manager**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\System`
*   Add:

    ```
    DWORD: DisableTaskMgr = 1
    ```

***

#### 22. **Disable Notification Center (Action Center)**

* **Path:**\
  `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Explorer`
*   Add:

    ```
    DWORD: DisableNotificationCenter = 1
    ```

***

#### 23. **Show Full Path in File Explorer Title Bar**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\CabinetState`
*   Add:

    ```
    String Value: FullPath = 1
    ```

***

#### 24. **Disable Cortana Completely**

* **Path:**\
  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search`
*   Add:

    ```
    DWORD: AllowCortana = 0
    ```

***

#### 25. **Clear Pagefile at Shutdown (For Forensics Privacy)**

* **Path:**  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management`
*   Add:

    ```
    DWORD: ClearPageFileAtShutdown = 1
    ```

***

#### 26. **Force Classic Volume Mixer**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\MTCUVC`
* Create `DWORD: EnableMtcUvc = 0`

***

#### 27. **Disable SmartScreen Filter**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\System`
*   Add:

    ```
    DWORD: EnableSmartScreen = 0
    ```

***

#### 28. **Disable “Low Disk Space” Warnings**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`
*   Add:

    ```
    DWORD: NoLowDiskSpaceChecks = 1
    ```

***

#### 29. **Custom DNS Settings (Force via Registry)**

*   **Path:**

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\<YourInterfaceGUID>
    ```
*   Add:

    ```
    String: NameServer = 1.1.1.1,8.8.8.8
    ```

***

#### 30. **Disable Video Previews in Explorer Thumbnails**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
*   Add:

    ```
    DWORD: DisablePreviewHandlers = 1
    ```

***

#### 31. **Remove “3D Objects” from File Explorer**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace`
*   Delete:

    ```
    {0DB7E03F-FC29-4DC6-9020-FF41B59E513A}
    ```

***

#### 32. **Enable Classic Volume Mixer (Taskbar Shortcut)**

*   Create a shortcut with this target:

    ```
    sndvol.exe -f
    ```
* Pin it to Taskbar for instant classic volume control.

***

#### 33. **Enable Verbose Boot (Detailed Startup Messages)**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`
*   Add:

    ```
    DWORD: VerboseStatus = 1
    ```

***

#### 34. **Disable Windows Startup Sound**

* **Path:**  `HKEY_CURRENT_USER\AppEvents\EventLabels\WindowsLogon`
*   Set:

    ```
    ExcludeFromCPL = 1
    ```

***

#### 35. **Enable Enhanced Search Indexing**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Search`
*   Set:

    ```
    DWORD: EnableDynamicContentIndexer = 1
    ```

***

#### 36. **Remove Search Box from Taskbar via Registry**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Search`
*   Add:

    ```
    DWORD: SearchboxTaskbarMode = 0
    ```

***

#### 37. **Disable Auto-Reboot After Updates**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU`
*   Add:

    ```
    DWORD: NoAutoRebootWithLoggedOnUsers = 1
    ```

***

#### 38. **Remove Action Center (Notifications Flyout)**

* **Path:**  `HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Explorer`
*   Add:

    ```
    DWORD: DisableNotificationCenter = 1
    ```

***

#### 39. **Enable Hidden Clipboard Format View (For Debugging)**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Clipboard`
*   Add:

    ```
    DWORD: EnableFormatView = 1
    ```

***

#### 40. **Pin Any App to Taskbar via Registry (Manually)**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Taskband`
* You can manually edit/pin apps here (complex binary – advanced use only)

***

#### 41. **Force All File Extensions to Show**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
*   Set:

    ```
    DWORD: HideFileExt = 0
    ```

***

#### 42. **Disable Windows Defender Tamper Protection**

> Warning: Defender will try to re-enable this automatically.

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Features`
*   Add:

    ```
    DWORD: TamperProtection = 0
    ```

***

#### 43. **Enable Hidden Developer Search Mode**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\SearchSettings`
*   Add:

    ```
    DWORD: IsDeviceSearchHistoryEnabled = 1
    ```

***

#### 44. **Enable Legacy System Tray Clock UI**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell\Update\Packages`
*   Add:

    ```
    DWORD: UndockingDisabled = 1
    ```

***

#### 45. **Disable Wallpaper Compression (Full Quality Desktop)**

* **Path:**  `HKEY_CURRENT_USER\Control Panel\Desktop`
*   Add:

    ```
    DWORD: JPEGImportQuality = 100
    ```

***

#### 46. **Enable “Dark Mode” Globally (System + Apps)**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Themes\Personalize`
*   Add:

    ```
    DWORD: AppsUseLightTheme = 0
    DWORD: SystemUsesLightTheme = 0
    ```

***

#### 47. **Enable Classic Alt+Tab Switcher**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer`
*   Add:

    ```
    DWORD: AltTabSettings = 1
    ```

***

#### 48. **Disable Modern Share UI (Restore Legacy)**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer`
*   Add:

    ```
    DWORD: DisableModernSharing = 1
    ```

***

#### 49. **Disable Sticky Keys Prompt**

* **Path:**  `HKEY_CURRENT_USER\Control Panel\Accessibility\StickyKeys`
*   Set:

    ```
    Flags = 506
    ```

***

#### 50. **Disable Auto Folder Type Discovery**

* **Path:**  `HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell\Bags\AllFolders\Shell`
*   Add:

    ```
    String: FolderType = NotSpecified
    ```

***

51\. **Enable Classic Right-Click Menu (Context Menu)**

* **Path:**  `HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32`
*   Set:

    ```
    (Default) = "" (empty string)
    ```

> Restart **Explorer.exe** after applying. Restores Windows 10-style right-click.

***

#### 52. **Force Show "This PC" on Desktop**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\HideDesktopIcons\NewStartPanel`
*   Set:

    ```
    DWORD: {20D04FE0-3AEA-1069-A2D8-08002B30309D} = 0
    ```

***

#### 53. **Disable Auto-Play Completely**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`
*   Add:

    ```
    DWORD: NoDriveTypeAutoRun = 0xFF
    ```

***

#### 54. **Hide All Desktop Icons**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`
*   Add:

    ```
    DWORD: NoDesktop = 1
    ```

***

#### 55. **Disable Hibernation (Also Deletes hiberfil.sys)**

*   Open CMD as Admin:

    ```
    powercfg -h off
    ```
*   Alternative:

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power
    HibernateEnabled = 0 (DWORD)
    ```

***

#### 56. **Change Taskbar Network Icon to Classic**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\NetworkList`
*   Add:

    ```
    DWORD: ReplaceSystemTrayNetwork = 1
    ```

***

#### 57. **Speed Up Shutdown**

* **Path:**  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`
*   Set:

    ```
    WaitToKillServiceTimeout = 2000
    ```

> Value is in **milliseconds** – default is 5000 or more.

***

#### 58. **Disable UI Animations for Performance**

* **Path:**  `HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics`
*   Set:

    ```
    MinAnimate = 0
    ```

***

#### 59. **Require Ctrl + Alt + Del to Login**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon`
*   Set:

    ```
    DWORD: DisableCAD = 0
    ```

***

#### 60. **Enable Desktop Slideshow (Even When on Battery)**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Slideshow`
*   Add:

    ```
    DWORD: SlideshowEnabledOnBattery = 1
    ```

***

#### 61. **Enable Precision Touchpad Hidden Features**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\PrecisionTouchPad\Status`
*   Add:

    ```
    DWORD: Enabled = 1
    ```

***

#### 62. **Disable "Shake to Minimize" Feature**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
*   Add:

    ```
    DWORD: DisallowShaking = 1
    ```

***

#### 63. **Set Custom Lock Screen Image via Registry**

* **Path:**  `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Personalization`
*   Add:

    ```
    String: LockScreenImage = "C:\Path\To\Your\Image.jpg"
    ```

***

#### 64. **Set Battery Saver Threshold**

* **Path:**  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\PowerThrottling`
*   Add:

    ```
    DWORD: BatterySaverThreshold = 30
    ```

***

#### 65. **Enable Rich Clipboard History**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Clipboard`
*   Add:

    ```
    DWORD: EnableClipboardHistory = 1
    ```

***

#### 66. **Force Desktop Background Fit Mode**

* **Path:**  `HKEY_CURRENT_USER\Control Panel\Desktop`
*   Set:

    ```
    WallpaperStyle = 6 (Fit)
    TileWallpaper = 0
    ```

***

#### 67. **Enable "Do Not Disturb" Mode by Default**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Notifications\Settings`
*   Set:

    ```
    DWORD: NOC_GLOBAL_SETTING_ALLOW_TOASTS_ABOVE_LOCK = 0
    ```

***

#### 68. **Hide Drives in File Explorer**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`
*   Add:

    ```
    DWORD: NoDrives = 0x04 (example: hides drive D)
    ```

> Use bitmask: A=1, B=2, C=4, D=8, E=16, etc.

***

#### 69. **Enable Game Mode Registry Switch**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\GameBar`
*   Add:

    ```
    DWORD: AutoGameModeEnabled = 1
    ```

***

#### 70. **Reduce Menu Show Delay**

* **Path:**  `HKEY_CURRENT_USER\Control Panel\Desktop`
*   Set:

    ```
    MenuShowDelay = 0
    ```

***

#### 71. **Force Default Apps via Registry**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.txt\UserChoice`
*   Set:

    ```
    Progid = Applications\notepad.exe
    ```

***

#### 72. **Set File Explorer to Open Specific Folder**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`
*   Set:

    ```
    LaunchTo = 1 (Quick Access), 2 (This PC), or 3 (Home)
    ```

***

#### 73. **Enable Clipboard Sync Across Devices**

* **Path:**  `HKEY_CURRENT_USER\Software\Microsoft\Clipboard`
*   Add:

    ```
    DWORD: CloudClipboardFeatureEnabled = 1
    ```

***

#### 74. **Disable Password Reveal Button on Login**

* **Path:**  `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\CredUI`
*   Add:

    ```
    DWORD: DisablePasswordReveal = 1
    ```

***

#### 75. **Enable Ultimate Performance Power Plan (Hidden)**

*   Run this in **Admin CMD**:

    ```
    powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
    ```

***
