---
layout:     post
title:      "数据库每日自动备份"
subtitle:   ""
date:       2016-07-12
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
tags:
    - Powershell
---
>数据库的备份使用Sql Server Job来执行

### 备份数据库

```sql
DECLARE @SQLStatement VARCHAR(2000)
SET @SQLStatement = 'S:\DbTemp\Dfyf.Bpm.bak'
BACKUP DATABASE [Dfyf.Bpm] TO  DISK = @SQLStatement;
```

### 压缩数据库到指定目录

```powershell
Add-Type -Assembly "System.IO.Compression.FileSystem" ;
[System.IO.Compression.ZipFile]::CreateFromDirectory("S:\DbTemp\", "S:\DbBackUp\Dfyf.Bpm.bak.zip");
$fileName = 'S:\DbBackUp\Dfyf.Bpm.bak.zip'
$fileObj = get-item $fileName
# Get the date
$DateStamp = get-date -uformat "%Y-%m-%d@%H-%M-%S"
$extOnly = $fileObj.extension

if ($extOnly.length -eq 0) {
   $nameOnly = $fileObj.Name
   rename-item "$fileObj" "$nameOnly-$DateStamp"
   }
else {
   $nameOnly = $fileObj.Name.Replace( $fileObj.Extension,'')
   rename-item "$fileName" "$nameOnly-$DateStamp$extOnly"
   }
Remove-Item S:\DbTemp\Dfyf.Bpm.bak
```

### 删除指定目录下创建日期大于某个天数的文件

```powershell
function Remove-FilesCreatedBeforeDate([parameter(Mandatory)][ValidateScript({Test-Path $_})][string] $Path, [parameter(Mandatory)][DateTime] $DateTime, [switch] $DeletePathIfEmpty, [switch] $OutputDeletedPaths, [switch] $WhatIf)
{
    Get-ChildItem -Path $Path -Recurse -Force -File | Where-Object { $_.CreationTime -lt $DateTime } |
        ForEach-Object { if ($OutputDeletedPaths) { Write-Output $_.FullName } Remove-Item -Path $_.FullName -Force -WhatIf:$WhatIf }
    Remove-EmptyDirectories -Path $Path -DeletePathIfEmpty:$DeletePathIfEmpty -OnlyDeleteDirectoriesCreatedBeforeDate $DateTime -OutputDeletedPaths:$OutputDeletedPaths -WhatIf:$WhatIf
}
Remove-FilesCreatedBeforeDate -Path "C:\Some\Directory" -DateTime ((Get-Date).AddDays(-30)) -DeletePathIfEmpty
```
