
# 🔤 PowerShell Syntax & Fundamentals

This guide expands on the basics by introducing core PowerShell concepts like variables, logic, loops, and pipelines. This page is designed to be beginner-friendly and explain what each piece does.

---

## 📌 1. Variables

Variables in PowerShell **store data** (text, numbers, objects, arrays, etc.) and always start with a `$`.

```powershell
$name = "Alice"
$age = 32
$isAdmin = $true
```

### 📝 Notes
- Strings are in quotes: `"text"`
- Booleans: `$true` / `$false`
- Arrays use `@()` like so:
  ```powershell
  $colors = @("Red", "Blue", "Green")
  ```

---

## 🧮 2. Operators

### Arithmetic
```powershell
$sum = 2 + 2       # 4
$diff = 10 - 3     # 7
$product = 4 * 2   # 8
```

### Comparison
Used in logic like `if` statements:
```powershell
$a -eq $b    # equal
$a -ne $b    # not equal
$a -lt $b    # less than
$a -gt $b    # greater than
```

---

## 🔁 3. Loops

### For Loop
```powershell
for ($i = 0; $i -lt 5; $i++) {
    Write-Output "Number: $i"
}
```

### While Loop
```powershell
$count = 1
while ($count -le 3) {
    Write-Output "Loop $count"
    $count++
}
```

### Foreach Loop
```powershell
$users = @("Alice", "Bob", "Charlie")
foreach ($user in $users) {
    Write-Output "Hello $user"
}
```

---

## ✅ 4. If / Else

```powershell
if ($age -ge 18) {
    "Adult"
} elseif ($age -lt 18) {
    "Minor"
} else {
    "Unknown"
}
```

### Notes
- Comparison operators must be used (`-eq`, `-lt`, etc.)
- Braces `{}` are required to group commands

---

## 🧰 5. Functions

Functions let you reuse logic and take input parameters.

```powershell
function Say-Hello {
    param($name)
    Write-Output "Hello, $name!"
}

Say-Hello -name "Kyle"
```

---

## 🔗 6. Pipelines

PowerShell passes **objects** from one command to the next using pipes (`|`).

```powershell
Get-Service | Where-Object { $_.Status -eq "Running" }
```

### Explanation:
- `Get-Service` gets all services
- `Where-Object` filters based on a condition
- `$_` refers to the **current object** in the pipeline

---

## 💡 7. Script Blocks

A script block is a block of code stored as an object.

```powershell
$math = { param($x) $x * 10 }
& $math 5   # 50
```

---

## 📘 8. Comments

Use `#` for single-line comments:

```powershell
# This is a comment
Write-Output "Hello"
```

---

## 🧠 Tips

- Use `Tab` to autocomplete commands and paths
- Use `Get-Help` to get built-in documentation:
  ```powershell
  Get-Help Get-Service -Full
  ```

---

## 🚀 Keep Going

Next, try writing your own script file (`.ps1`), or explore:
- [Disk and Service Tools](../system/Disk_and_Service_Tools.md)
- [Bulk Operations](../ad/Bulk_Operations.md)

