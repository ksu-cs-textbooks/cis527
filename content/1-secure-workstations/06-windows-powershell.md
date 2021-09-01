---
title: "Windows 10 PowerShell"
weight: 30
pre: "6. "
---

{{< youtube OQufqVp7Eq0 >}}

#### Resources

* [Getting Started with Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1) from Microsoft
* [PowerShell Documentation](https://docs.microsoft.com/en-us/powershell/) from Microsoft
* [What is PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1) from Microsoft
* [Sample PowerShell Scripts](https://docs.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.1) from Microsoft
* [PowerShell Community Blog](https://devblogs.microsoft.com/powershell-community/) from Microsoft
* [Hey, Scripting Guy! Blog](https://blogs.technet.microsoft.com/heyscriptingguy/) from Microsoft (older content)

#### Video Script

Before digging too deep into Windows, let's take some time to learn about one of its most powerful, and least used, features, the PowerShell command line interface. PowerShell is an update to the old Command Prompt terminal, which was a very limited version of the DOS terminal from decades ago.

PowerShell is built on top of the .NET framework, and can leverage many features of that programming environment to perform powerful tasks within a simple interface. While we won't go too deep into PowerShell in this class, it is a very useful thing to learn.

On your Windows 10 Virtual Machine, you can open PowerShell by searching for it on the Start Menu.

The PowerShell interface is very simple, with just a small terminal that you can use to enter commands. Most commands take the form of a verb, followed by a hyphen, and then a noun. Let's try a few to see how they work:

* `Get-Location` - get the current directory
* `Set-Location <path>` - change directory
* `Get-ChildItem` - list files
* `New-Item <name> (-ItemType <"file" | "directory"> -Value <value>)` - make a new directory or file
* `Get-Content <name>` - get file contents
* `Remove-Item <name>` - remove a directory or file
* `Copy-Item <name>` - copy a directory or file
* `Move-Item <name>` - move a directory or file
* `Select-String -Pattern <pattern> -Path <path>` - search for a string in a file or group of files
* `Get-Command` - get a list of commands
* `Get-Help` - get help for a command
* `Get-Alias` - get a list of aliases for a command
* `Out-File` - output to a file

If you want to use the output of one command as input to another command, you can use the vertical pipe character `|` between commands. Here are some examples.

* `Select-String` - search for a string in output
* `Measure-Object <-Line | -Character | -Word>` - get line, word or character count
* `Sort-Object` - sort output by a property
* `Where-Object` - filter output by a property

You can also use PowerShell to write and execute scripts of commands. It is very similar to writing code in a programming language, but it is outside of the scope of this class. If you are interested in learning more, there are many great resources linked below the video to get you started. You can also check out the crash-course on PowerShell scripting in the Extras module.
