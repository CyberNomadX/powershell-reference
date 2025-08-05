
# 💽 Disk and Service Tools (PowerShell)

PowerShell commands and examples for working with disks, volumes, and Windows services. Useful for system maintenance, troubleshooting, and automation.

---

## 💿 Disk Management

### List All Volumes
```powershell
Get-Volume
```

### List All Disks
```powershell
Get-Disk
```

### Initialize a Disk
```powershell
Initialize-Disk -Number 1
```

### Create a New Partition
```powershell
New-Partition -DiskNumber 1 -UseMaximumSize -AssignDriveLetter
```

### Format a Partition
```powershell
Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "Data"
```

---

## 🔁 Rescan Disks
```powershell
Update-HostStorageCache
```

---

## 🧰 Check Disk Health
```powershell
Get-PhysicalDisk | Select-Object FriendlyName, OperationalStatus, HealthStatus, Size
```

---

## 🛠️ Service Management

### List All Services
```powershell
Get-Service
```

### Get Status of a Specific Service
```powershell
Get-Service -Name "wuauserv"
```

### Start/Stop/Restart a Service
```powershell
Start-Service -Name "wuauserv"
Stop-Service -Name "wuauserv"
Restart-Service -Name "wuauserv"
```

### Set Service to Automatic or Manual
```powershell
Set-Service -Name "wuauserv" -StartupType Automatic
Set-Service -Name "wuauserv" -StartupType Manual
```

---

## 📄 Export Services to CSV
```powershell
Get-Service | Select-Object Name,Status,DisplayName | Export-Csv -Path ".\Services.csv" -NoTypeInformation
```
