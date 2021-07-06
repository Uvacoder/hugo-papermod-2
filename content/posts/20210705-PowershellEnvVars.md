---
draft: false
title: Powershell Environment Variables Configuration
description: Configuring Environment Variables with Powershell

date: 2021-07-06T19:00:00+01:00
tags: 
    - Powershell
    - QuickHacks
categories:
    - Powershell
    - Windows
---
Really quick, but handy and cool script to sort your environment variable - `$env:path` - using .NET Methods and powershell (Tested on Powershell  5.1 and 7.1.3)

**The usual disclaimer** - don't cock around here if you don't know what your doing, you can make things go all kinds of weird and it's a PITA to fix. Take a copy before making any changes. Don't be stupid.

## System Wide Environment Variable

This will set the system environment var and needs admin powers.
```
$folderToAdd = "C:\someFolder\"
#Set it at a system level (HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment)
[System.Environment]::SetEnvironmentVariable("Path", [System.Environment]::GetEnvironmentVariable('Path', [System.EnvironmentVariableTarget]::Machine ) + ";" + "$folderToAdd", [System.EnvironmentVariableTarget]::Machine)
```

## User Space Environment Variable
Since at least win10, We can also set it at a user level - this can be dead useful as it doesn't require an admin powershell
```
$folderToAdd = "C:\someFolder\"
#Set it at a user level (HKEY_CURRENT_USER\Environment)
[System.Environment]::SetEnvironmentVariable("Path", [System.Environment]::GetEnvironmentVariable('Path', [System.EnvironmentVariableTarget]::User ) + ";" + "$folderToAdd", [System.EnvironmentVariableTarget]::User)
```