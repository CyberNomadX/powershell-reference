
# 🔄 Bulk Operations in Active Directory (PowerShell)

PowerShell scripts and examples for performing bulk actions in Active Directory using CSV files or batch processing. Ideal for onboarding, offboarding, and audits.

---

## 👤 Bulk Create Users from CSV

### CSV Format
```csv
Name,SamAccountName,UserPrincipalName,OU
John Doe,jdoe,jdoe@example.com,OU=Staff,DC=example,DC=com
Jane Smith,jsmith,jsmith@example.com,OU=Staff,DC=example,DC=com
```

### PowerShell Script
```powershell
Import-Csv .\users.csv | ForEach-Object {
    New-ADUser -Name $_.Name `
               -SamAccountName $_.SamAccountName `
               -UserPrincipalName $_.UserPrincipalName `
               -Path $_.OU `
               -AccountPassword (ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force) `
               -Enabled $true
}
```

---

## 👥 Bulk Add Users to a Group

### CSV Format
```csv
SamAccountName
jdoe
jsmith
```

### PowerShell Script
```powershell
$group = "HR Staff"
Import-Csv .\group_members.csv | ForEach-Object {
    Add-ADGroupMember -Identity $group -Members $_.SamAccountName
}
```

---

## 🔐 Bulk Reset Passwords

```powershell
Import-Csv .\users.csv | ForEach-Object {
    Set-ADAccountPassword -Identity $_.SamAccountName -Reset `
        -NewPassword (ConvertTo-SecureString "NewP@ssw0rd!" -AsPlainText -Force)
}
```

---

## ❌ Bulk Disable Accounts

```powershell
Import-Csv .\users.csv | ForEach-Object {
    Disable-ADAccount -Identity $_.SamAccountName
}
```

---

## 📂 Bulk Move Users to New OU

```powershell
Import-Csv .\users.csv | ForEach-Object {
    Move-ADObject -Identity "CN=$($_.SamAccountName),OU=OldOU,DC=example,DC=com" `
                  -TargetPath "OU=NewOU,DC=example,DC=com"
}
```

---

## 📄 Export All Users to CSV

```powershell
Get-ADUser -Filter * -Property SamAccountName,Name,EmailAddress |
Select-Object SamAccountName,Name,EmailAddress |
Export-Csv -Path ".\AllUsers.csv" -NoTypeInformation
```
