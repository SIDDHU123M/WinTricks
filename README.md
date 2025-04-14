# Welcome

## Windows 11 Secrets, Tweaks, and Power Tricks

A curated collection of **100+ hidden features**, **registry hacks**, **keyboard shortcuts**, and **advanced system tricks** for Windows 11 — to boost productivity, customize deeply, and unlock powerful controls.

***

### 📌 Disclaimer

> ⚠️ Not all tweaks work on every device or Windows 11 build. Some may depend on specific hardware (e.g., touchpad, battery), OEM restrictions, or Group Policy settings.\
> Always **create a system restore point** or **back up your registry** before applying changes. Test carefully and use at your own risk.

***

### 🧩 Categories

#### ✅ Safe Tweaks (No Registry)

* Power keyboard shortcuts
* System tools & utilities
* Command-line tricks
* Hidden gesture controls
* Productivity enhancements

#### 🧠 Registry Tweaks

* UI & UX modifications (classic right-click, taskbar position)
* Performance boosts (faster shutdowns, menu delay)
* Hidden OS settings (disable auto-play, password reveal button)
* Explorer, desktop, and personalization customizations

***

### Backup Before Tweaking

#### 🔹 Registry Backup Script

Run the following `.bat` file to export current registry safely:

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
