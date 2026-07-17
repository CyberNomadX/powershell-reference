
# 🧠 PowerShell for Absolute Beginners

This guide covers the very basics of PowerShell—what it is, how to use it, and how to understand the core concepts before diving into scripting.

---

## 💡 What is PowerShell?

PowerShell is a **command-line shell** and **scripting language** built by Microsoft.  
It lets you manage and automate nearly every part of Windows—and even works on Linux and macOS.

It’s:
- Object-based (not just text)
- Integrated with .NET
- Extremely powerful for system admins

---

## 📟 Opening PowerShell

To start PowerShell:

- On Windows: Press `Windows + X`, then select **Windows PowerShell** or **Terminal**
- Or type `powershell` into the Start menu

You’ll see a prompt that looks like:
```
PS C:\Users\YourName>
```

You’re now in the PowerShell environment.

---

## 🔹 Running Commands

PowerShell works by typing in **commands** (called *cmdlets*):

```powershell
Get-Date
```

This shows the current date and time.

```powershell
Get-Process
```

Shows all running processes.

```powershell
Get-Service
```

Lists all system services.

Most cmdlets follow the **Verb-Noun** format:
```
Get-Item
Set-ExecutionPolicy
New-LocalUser
```

---

## 🧪 Try This

Type each of these into PowerShell and press Enter:

```powershell
Get-Location      # Shows your current folder
Get-ChildItem     # Lists files/folders (like 'ls' or 'dir')
Clear-Host        # Clears the screen
```

---

## 🧠 Cmdlet Breakdown

Let’s break down one:

```powershell
Get-ChildItem -Path C:\Windows -Recurse
```

- `Get-ChildItem`: the main command
- `-Path`: tells it where to look
- `-Recurse`: includes subfolders

This command lists **every file** in `C:\Windows` and its subfolders.

---

## ⚙️ Tab Completion

Type the first few letters of a command and hit `Tab`:
```powershell
Get-Pro [Tab] → Get-Process
```

Same works for parameter names and paths:
```powershell
Get-ChildItem -Pat [Tab]
```

---

## 📌 Summary

| Feature         | Example             |
|----------------|---------------------|
| View time      | `Get-Date`          |
| List files     | `Get-ChildItem`     |
| Check folder   | `Get-Location`      |
| Clear screen   | `Clear-Host`        |
| View services  | `Get-Service`       |

---

## ✅ Next Steps

Once you're comfortable running simple commands, you can move on to:
- [Variables and Logic](Syntax_and_Fundamentals.md)
- [Disk and Service Tools](../system/Disk_and_Service_Tools.md)
- [Active Directory](../ad/Active_Directory.md)
