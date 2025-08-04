
# 📜 Group Policy Management (PowerShell)

PowerShell commands for managing Group Policy Objects (GPOs). Useful for auditing, deployment, and automation in Active Directory environments.

---

## 📋 List All GPOs
```powershell
Get-GPO -All
```

---

## 🔍 Get GPO Details
```powershell
Get-GPO -Name "Default Domain Policy"
```

---

## 🔗 Link GPO to an OU
```powershell
New-GPLink -Name "IT Policy" -Target "OU=IT,DC=example,DC=com" -LinkEnabled Yes
```

---

## 🔗 Remove GPO Link
```powershell
Remove-GPLink -Name "IT Policy" -Target "OU=IT,DC=example,DC=com"
```

---

## 💾 Backup a GPO
```powershell
Backup-GPO -Name "IT Policy" -Path "C:\GPOBackups"
```

---

## ♻️ Restore a GPO
```powershell
Restore-GPO -Name "IT Policy" -Path "C:\GPOBackups"
```

---

## 📦 Import GPO Settings from Backup
```powershell
Import-GPO -BackupGpoName "IT Policy" -Path "C:\GPOBackups" -TargetName "Imported IT Policy"
```

---

## 🧪 Test GPO Application on a Computer
```powershell
gpresult /S PC-001 /USER domain\username /H report.html
```

---

## 🔁 Force Group Policy Update Remotely
```powershell
Invoke-GPUpdate -Computer "PC-001" -Force
```

---

## 📄 Export GPO Settings to HTML
```powershell
Get-GPOReport -Name "IT Policy" -ReportType Html -Path "C:\Reports\ITPolicy.html"
```
