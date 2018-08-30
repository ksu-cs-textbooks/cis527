---
title: "5. PowerShell Scripting"
date: 2018-08-24T10:53:26-05:00
---

{{< youtube j8vDSs2mDeM >}}

#### Resources

* [Windows PowerShell: Scripting Crash Course](https://technet.microsoft.com/en-us/library/hh551144.aspx) from Microsoft TechNet
* [How to Write and Run Scripts in the Windows PowerShell ISE](https://docs.microsoft.com/en-us/powershell/scripting/core-powershell/ise/how-to-write-and-run-scripts-in-the-windows-powershell-ise?view=powershell-6) from Microsoft
* [Windows PowerShell Scripting Tutorial for Beginners](https://blog.netwrix.com/2018/02/21/windows-powershell-scripting-tutorial-for-beginners/) from Netwrix

#### Video Transcript

This video introduces the Windows PowerShell Integrated Scripting Environment (ISE) and covers the basics for creating and running your own scripts in Windows PowerShell.

Before we begin, we must change one system setting to allow unsigned PowerShell scripts to run. To do this, you'll need to open a PowerShell window using the Run as Administrator option, and then enter the following command:

```powershell
Set-ExecutionPolicy Unrestricted
```

However, be aware that this makes your system a bit more vulnerable. If you or a malicious program tries to run a malicious PowerShell script that is unsigned, the system will not try to stop you. It would be a very rare occurrence, but it is something to be aware of.

Now, let's open the PowerShell ISE to start writing scripts. To find it, simply search for PowerShell ISE on your Start Menu. It should be included by default on all versions of Windows 10.

When you first open the PowerShell ISE, you may have to click the Script button in the upper-right corner of the window to view both the scripting pane and the command window. To write your scripts, you can simply write the text in the upper window, then save the file and run the program using the Run script button on the top toolbar. You can also run the script in the command window below.

To begin, let's take a look at a simple Hello World script:

```powershell
Write-Host "Hello World"
return
```

This script should be pretty self-explanatory. The `Write-Host` command simply displays text on the terminal, and the return line ends the script. As with any programming language, it is good practice to include a return at the end of your script, but it is not necessarily required.

Let's look at a more advanced script to see more features of the Windows PowerShell scripting language.

```powershell
Param(
    [string]$user
)

if ( -not ($user)){
    Write-Host "Usage: batman.ps1 <name>"
    return
}

if ($user.CompareTo("Batman") -eq 0){
    Write-Host "Hello Mr. Wayne"
}else{
    if ($user.CompareTo("Robin") -eq 0){
        Write-Host "Welcome back Mr. Grayson"
    }else{
        Write-Host "Intruder alert!"
    }
}
return
```

At the top of this script, there is a special `Param` section. In PowerShell, any parameters expected from the user must be declared here, with the data type in square brackets (`[` and `]`), followed by the variable name prefixed with a dollar sign `$`. In this script, we have declared one command line parameter `$user` of type string.

Below that, we have the first if statement:

```powershell
if ( -not ($user)){
    Write-Host "Usage: batman.ps1 <name>"
    return
}
```
This will check to see if the `$user` parameter was provided. If it was not, it will print an error message and return to end the script.

The next if statement:

```powershell
if ($user.CompareTo("Batman") -eq 0){
    Write-Host "Hello Mr. Wayne"
}else{
    if ($user.CompareTo("Robin") -eq 0){
        Write-Host "Welcome back Mr. Grayson"
    }else{
        Write-Host "Intruder alert!"
    }
}
```

performs a string comparison between the `$user` parameter and the string "Batman", if the comparison returns `0`, they are equal. This is very similar to other string comparison functions in C# and Java. One interesting item to note here is the use of `-eq` to denote equality. For some reason, PowerShell uses short textual comparison operators instead of the common symbols for boolean comparisons. I really don't know why that particular design decision was made, but I encourage you to look at the documentation to see what options are available for comparison.

Here is another simple script:

```powershell
Param(
    [string]$path
)

$files = Get-ChildItem $path

foreach($file in $files){
    Write-Host $file.name
}
```

This is an example of a simple looping script. In this script, it will get a path from the user as an argument, then store a list of all the child items on that path in `$files` variable. Then, it will use a "foreach" loop to print out the name of each of those files. Thankfully, if you've done any programming in the .NET family of languages, most of this syntax will be very familiar to you.

You can also use PowerShell to create a simple menu for your script. This is a bit more involved than the example from the Linux Bash scripting video, but it is pretty straightforward:

```powershell
$title = "Select Options"
$message = "Choose an option to perform"

$build = New-Object System.Management.Automation.Host.ChoiceDescription "&Build", "Build the project"
$run = New-Object System.Management.Automation.Host.ChoiceDescription "&Run", "Run the project"
$clean = New-Object System.Management.Automation.Host.ChoiceDescription "&Clean", "Clean the project"
$quit = New-Object System.Management.Automation.Host.ChoiceDescription "&Quit", "Quit"

$options = [System.Management.Automation.Host.ChoiceDescription[]]($build, $run, $clean, $quit)

$result = $host.ui.PromptForChoice($title, $message, $options, 0)
switch ($result)
{
    0 {
        Write-Host "You selected Build"
    }
    1 {
        Write-Host "You selected Run"
    }
    2 {
        Write-Host "You selected Clean"
    }
    3 {
        Write-Host "You selected Quit"
    }
}
```

At the top of the script, the first two variables define the text that will be shown as the title of the menu and the message displayed to the user before the menu options. The next four variables define the menu choices available. Looking at the first one, the `&Build` gives the title of the option, with the ampersand `&` before the 'B' indicating which letter should be the shortcut to choose that option. The next string gives a longer description of the option. Finally, we put it all together in the `$options` variable as an array of available options, then use the PromptForChoice function to display the menu to the user, storing the user's choice in the `$result` variable. Finally, we use a simple "switch" statement to determine which option the user chose and then perform that task.

If you are having trouble understanding what each part does, I recommend just running the script once and then matching up the text displayed in the menu with the script's code. It may seem a bit daunting at first, but it is actually pretty simple overall. As a quick aside, if you run this on a system with a GUI, you may get an actual pop-up menu instead of a textual menu, but rest assured that it will display the textual version on system's without a GUI.

Finally, here is a quick script demonstrating how to get user input directly within the script:

```powershell
$name = Read-Host "Input your name and press [ENTER]"
Write-Host "Welcome $name!"
```

It's as simple as that! Of course, that is just a very small taste of what PowerShell is capable of. Hopefully this introduction gives you some idea of what is available, but I encourage you to consult the online documentation for PowerShell to learn even more about it.
