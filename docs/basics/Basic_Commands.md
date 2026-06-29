# Basic PowerShell Commands

> **Work in progress** — still needs to be organized. TODO: figure out a page-specific search function.

## Check if file exists
To check if a file exists, use the `Test-Path` command.

**Example:**
```powershell
Test-Path -Path "C:\path\to\your\file.txt"
```

**Return values:**
- File exists → `$True`
- File does not exist → `$False`
