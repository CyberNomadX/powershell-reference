# Basic PowerShell Commands

> **Work in progress** — still needs to be organized. TODO: figure out a page-specific search function.

## Check if file exists
To check if a file exists, use the `Test-Path` command.  
**Example:**
```powershell
Test-Path -Path "C:\path\to\your\file"
```

**Return values:**
- File exists → `$True`
- File does not exist → `$False`

## Using If Statements
Wrapping command with conditions for specifics depending on files presence.  
**Simple Example**  

```powershell
if (Test-Path -Path "C:\path\to\your\file") {  
    Write-Host "The file exists!"  
}  else {  
    Write-Host "The file is missing."  
}
```

