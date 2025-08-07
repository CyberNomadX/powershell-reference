
# 📁 Active Directory PowerShell Reference

PowerShell commands and examples for managing Active Directory. Useful for sysadmins working with domain controllers, users, groups, OUs, and GPOs.

---

## 🛠️ Prerequisites
```powershell
Import-Module ActiveDirectory
```

---

## 👤 User Management

### Create a New User
```powershell
New-ADUser -Name "John Doe" -SamAccountName jdoe -UserPrincipalName jdoe@example.com -Path "OU=Staff,DC=example,DC=com" -AccountPassword (Read-Host -AsSecureString "Set Password") -Enabled $true
```

### Reset Password
```powershell
Set-ADAccountPassword -Identity jdoe -Reset -NewPassword (Read-Host -AsSecureString "New Password")
```

### Enable/Disable Account
```powershell
Enable-ADAccount -Identity jdoe
Disable-ADAccount -Identity jdoe
```

### Move User to Another OU
```powershell
Move-ADObject -Identity "CN=John Doe,OU=Staff,DC=example,DC=com" -TargetPath "OU=IT,DC=example,DC=com"
```

---

## 🧑‍🤝‍🧑 Group Management

### Create a Group
```powershell
New-ADGroup -Name "HR Staff" -GroupScope Global -GroupCategory Security -Path "OU=Groups,DC=example,DC=com"
```

### Add/Remove User to/from Group
```powershell
Add-ADGroupMember -Identity "HR Staff" -Members jdoe
Remove-ADGroupMember -Identity "HR Staff" -Members jdoe -Confirm:$false
```

---

## 🏢 OU Management

### Create OU
```powershell
New-ADOrganizationalUnit -Name "IT" -Path "DC=example,DC=com"
```

### Rename OU
```powershell
Rename-ADObject -Identity "OU=OldName,DC=example,DC=com" -NewName "NewName"
```

---

## 🔍 Searching & Filtering

### Find a User by Name
```powershell
Get-ADUser -Filter 'Name -like "*john*"' -Properties *
```

### List Disabled Accounts
```powershell
Get-ADUser -Filter 'Enabled -eq $false' -Properties Enabled
```

### Find Users Not Logged In for X Days
```powershell
Search-ADAccount -AccountInactive -UsersOnly -TimeSpan 90.00:00:00
```

---

## 🧪 Testing & Validation

### Check if User Exists
```powershell
Get-ADUser -Identity jdoe
```

### Test Group Membership
```powershell
Get-ADUser jdoe | Get-ADUserMemberOf
```

### Check AD trust relationship
```powershell
Test-ComputerSecureChannel
```
Returns ```True``` if the trust relationship is intact, or ```False``` if its broken.
Verbose output: ```-Verbose```
Force repair: ```Test-ComputerSecureChannel -Repair -Credential (Get-Credential)```
Remote (if powershell remoting is enabled):
```powershell
Invoke-Command -ComputerName RemotePCName -ScriptBlock { Test-ComputerSecureChannel }
```

---

## 📄 Exporting Results

### Export Users to CSV
```powershell
Get-ADUser -Filter * -Property Name,EmailAddress | Select-Object Name,EmailAddress | Export-Csv -Path ".\Users.csv" -NoTypeInformation
```

---

## 🔒 Password & Account Policies

### Force Password Change at Next Logon
```powershell
Set-ADUser jdoe -ChangePasswordAtLogon $true
```

### Unlock Account
```powershell
Unlock-ADAccount -Identity jdoe
```
