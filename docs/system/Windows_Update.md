
# 🪟 Windows Update with PowerShell

This guide provides a universal approach to managing Windows Updates using PowerShell—compatible with both client endpoints and servers.

---

## 📦 Install PSWindowsUpdate Module

Most advanced update tasks require the `PSWindowsUpdate` module, which works on both Windows clients and servers.

```powershell
Install-PackageProvider -Name NuGet -Force
Install-Module -Name PSWindowsUpdate -Force
Import-Module PSWindowsUpdate
```

> If prompted to trust the repository, type `Y`.

---

## 🔍 Check for Available Updates

```powershell
Get-WindowsUpdate
```

This checks for pending updates from Windows Update or WSUS depending on system configuration.

---

## 📥 Install Updates

```powershell
Install-WindowsUpdate -AcceptAll -AutoReboot
```

- `-AcceptAll`: Automatically approve updates
- `-AutoReboot`: Reboot automatically if required

For interactive use without auto reboot:

```powershell
Install-WindowsUpdate -AcceptAll
```

---

## 🔄 Check & Install in One Command

```powershell
Get-WindowsUpdate -Install -AcceptAll -AutoReboot
```

---

## 📋 List Installed Updates

Built-in alternative (does not require module):

```powershell
Get-HotFix
```

---

## ❌ Hide a Specific Update

```powershell
Hide-WindowsUpdate -KBArticleID "KB5009543" -Hide
```

---

## 🧪 Optional: Enable Script Execution

Required to run remote or downloaded scripts:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## 🕒 Schedule Automatic Update Task

Example: Run daily at 2 AM:

```powershell
$Trigger = New-ScheduledTaskTrigger -Daily -At 2am
$Action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "Install-WindowsUpdate -AcceptAll -AutoReboot"
Register-ScheduledTask -TaskName "AutoWindowsUpdate" -Trigger $Trigger -Action $Action -RunLevel Highest -User "SYSTEM"
```

---

## 🧠 Notes

- Works on Windows 10, 11, and Server 2016/2019/2022
- Will follow WSUS policies if domain-joined and configured
- Requires admin privileges

---

## 🔗 References

- PSWindowsUpdate GitHub: [https://github.com/mgrosvenor/PSWindowsUpdate](https://github.com/mgrosvenor/PSWindowsUpdate)
- Microsoft Docs: [Windows Update for Business](https://docs.microsoft.com/en-us/windows/deployment/update/)
