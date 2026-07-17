# File Commands

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

### Using If Statements
Wrapping command with conditions for specifics depending on files presence.  

**Simple Example:**  

```powershell
if (Test-Path -Path "C:\path\to\your\file") {  
    Write-Host "The file exists!"  
}  else {  
    Write-Host "The file is missing."  
}
```

**Breakdown Of Above**  
- The script effectively translates to "If the requested file is there then output this, otherwise output this".  
- This means that if you where to put the output "the file is missing" where the statement "The file exists!" then you will be told the file doesnt exsist every time the file is there.  

## Create Folders and Files

### Making Folders

***MKDIR Command***  
`mkdir` works on powershell and can be used to make folders
```powershell
mkdir "C:\path\to\desired\folder"
```

***PS Standard (New-Item)***  
The native method to create a folder is with `New-Item`  
```powershell
New-Item -Path "C:\path\you\want\folder" -Name "NewFolderName" -ItemType Directory
```

This method can also be used to make multiple folders at once:
```powershell
New-Item -ItemType Directory -Name "Docs", "Images", "Source"
```

