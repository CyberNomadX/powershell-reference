
# 🖥️ Computer Account Management (PowerShell)

PowerShell commands for managing computer accounts in Active Directory. Useful for provisioning, cleanup, and auditing.

---

## ➕ Create a New Computer Account
```powershell
New-ADComputer -Name "PC-001" -Path "OU=Computers,DC=example,DC=com" -Enabled $true
```

---

## 🔄 Rename a Computer Account
```powershell
Rename-ADObject -Identity "CN=OldName,OU=Computers,DC=example,DC=com" -NewName "NewName"
```

---

## 🏢 Move Computer to Another OU
```powershell
Move-ADObject -Identity "CN=PC-001,OU=OldOU,DC=example,DC=com" -TargetPath "OU=NewOU,DC=example,DC=com"
```

---

## ❌ Disable or Delete a Computer Account

### Disable
```powershell
Disable-ADAccount -Identity "PC-001"
```

### Delete
```powershell
Remove-ADComputer -Identity "PC-001" -Confirm:$false
```

---

## 🔍 Find Inactive Computer Accounts
```powershell
Search-ADAccount -AccountInactive -ComputersOnly -TimeSpan 90.00:00:00
```

---

## 📋 List All Computers in a Specific OU
```powershell
Get-ADComputer -Filter * -SearchBase "OU=Computers,DC=example,DC=com"
```

---

## 🧪 Get Computer Details
```powershell
Get-ADComputer -Identity "PC-001" -Properties *
```

---

## 🧼 Cleanup: Find Disabled Computer Accounts
```powershell
Get-ADComputer -Filter 'Enabled -eq $false'
```

---

## 📄 Export List of Computers to CSV
```powershell
Get-ADComputer -Filter * -Property Name,OperatingSystem | 
Select-Object Name,OperatingSystem | 
Export-Csv -Path ".\Computers.csv" -NoTypeInformation
```
