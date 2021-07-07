---
draft: False
title: Powershell Screen KeepAwake
description: Keeping your screen awake, with powershell!

date: 2021-07-07T11:00:00+01:00
tags: 
    - Powershell
    - QuickHacks
categories:
    - Powershell
    - Windows
---
So, there's occassions where the screen lock GPo gets in my way, so I came up with a quick powershell solution that hits a magical "F13" key.
I don't advocate running this in the office, or public spaces, but it's super handy at my home desk especially when I'm monitoring a system or process and not neccessarily hands on keys.

## Start-KeepAwake!

Open up your $profile in your favourite editor. Alternatively, you can bake this function into a module for import if your that way inclined.

Add the following:
```
Function Start-KeepAwake {

$Script = {$myshell = new-object -com "wscript.shell" ; while ($i -lt 1)  {$myshell.SendKeys("{F13}") ; Start-sleep -Seconds 90 }}

Start-Job -Name F13-KeepAwake -ScriptBlock $Script

}
```
It's really simple , it creates a new shell object, sets an infinite loop that presses `F13` every 90 seconds. This is then wrapped up in a Powershell Job, to return screen input.

To turn it off, either kill the job, or close your session! You could always create a `Stop-KeepAwake` function if you needed.
