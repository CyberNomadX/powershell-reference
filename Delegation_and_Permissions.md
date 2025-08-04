
# 🔐 Delegation & Permissions (PowerShell)

PowerShell commands to view, assign, and audit permissions and delegation in Active Directory. Useful for managing RBAC, compliance, and delegated OU control.

---

## 🔎 View ACL (Access Control List) of an OU
```powershell
$ou = "OU=IT,DC=example,DC=com"
(Get-Acl "AD:$ou").Access
```

---

## 👤 Delegate Permissions to a User on an OU

### Example: Allow `helpdeskuser` to reset passwords in the IT OU
```powershell
$identity = "OU=IT,DC=example,DC=com"
$rule = New-Object System.DirectoryServices.ActiveDirectoryAccessRule `
    (New-Object System.Security.Principal.NTAccount("example\helpdeskuser")),
    "ExtendedRight",
    "Allow",
    ([GUID]"00299570-246d-11d0-a768-00aa006e0529")  # Reset password right

$ou = [ADSI]"LDAP://$identity"
$ou.psbase.ObjectSecurity.AddAccessRule($rule)
$ou.psbase.CommitChanges()
```

---

## 🧾 View Effective Permissions

Active Directory does not natively support viewing effective permissions directly via PowerShell. Use GUI tools like **dsacls** or **Active Directory Users and Computers** with advanced permissions.

However, you can view **explicit permissions**:

```powershell
(Get-Acl "AD:OU=IT,DC=example,DC=com").Access |
Where-Object { $_.IdentityReference -like "*helpdeskuser*" }
```

---

## 🗃️ Export OU Permissions to a File
```powershell
$ou = "OU=IT,DC=example,DC=com"
(Get-Acl "AD:$ou").Access |
Select-Object IdentityReference, ActiveDirectoryRights, AccessControlType |
Export-Csv -Path ".\OU_Permissions.csv" -NoTypeInformation
```

---

## 🧼 Remove Specific Delegated Right

⚠️ Manual and careful process. Usually safer to do via GUI unless well-scripted.

---

## 📢 Tips

- Use `dsacls` for advanced ACL manipulation and viewing from the command line.
- Test any delegation changes in a non-production environment before applying.
