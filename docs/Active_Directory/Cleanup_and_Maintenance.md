
# 🧼 Active Directory Cleanup & Maintenance (PowerShell)

Useful PowerShell commands for identifying and cleaning up stale, unused, or misconfigured Active Directory objects. Ideal for regular audits and health checks.

---

## 🧍‍♂️ Find Disabled User Accounts
```powershell
Get-ADUser -Filter 'Enabled -eq $false'
```

---

## 🧍‍♀️ Find Users Who Haven’t Logged In Recently
```powershell
Search-ADAccount -AccountInactive -UsersOnly -TimeSpan 90.00:00:00
```

---

## 🖥️ Find Inactive Computer Accounts
```powershell
Search-ADAccount -AccountInactive -ComputersOnly -TimeSpan 90.00:00:00
```

---

## 🔒 Find Locked Out Accounts
```powershell
Search-ADAccount -LockedOut
```

---

## 🧑‍🤝‍🧑 Find Empty Groups
```powershell
Get-ADGroup -Filter * | Where-Object {
    @(Get-ADGroupMember $_.DistinguishedName).Count -eq 0
}
```

---

## 🏢 Find Empty OUs
```powershell
Get-ADOrganizationalUnit -Filter * | Where-Object {
    @(Get-ADObject -SearchBase $_.DistinguishedName -SearchScope OneLevel -Filter *).Count -eq 0
}
```

---

## 🆔 Find Duplicate SAM Account Names
```powershell
Get-ADUser -Filter * | Group-Object SamAccountName | Where-Object { $_.Count -gt 1 }
```

---

## 🧾 Export Inactive Users to CSV
```powershell
Search-ADAccount -AccountInactive -UsersOnly -TimeSpan 90.00:00:00 |
Select-Object Name,SamAccountName,LastLogonDate |
Export-Csv -Path ".\InactiveUsers.csv" -NoTypeInformation
```

---

## 🧰 Cleanup Tips
- Document all removals.
- Use `-WhatIf` to simulate destructive actions.
- Schedule regular reviews of inactive accounts.
- Use filters carefully in scripts to avoid accidental mass changes.
