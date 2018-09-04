---
title: "Bash Scripting"
weight: 15
pre: "3. "
---

{{< youtube yMU30kePPP8 >}}

#### Resources

* [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/index.html) from The Linux Documentation Project (TLDP)
* [Advanced Command Line How To](https://help.ubuntu.com/community/AdvancedCommandlineHowto) from Ubuntu
* [Beginners / Bash Scripting](https://help.ubuntu.com/community/Beginners/BashScripting) from Ubuntu
* [Environment Variables](https://help.ubuntu.com/community/EnvironmentVariables) from Ubuntu
* [Cron How To](https://help.ubuntu.com/community/CronHowto) from Ubuntu
* [Magic Number](https://en.wikipedia.org/wiki/File_format#Magic_number) on Wikipedia

#### Video Transcript

In this video, I'll introduce the concepts for scripting using the Bash shell in Ubuntu Linux. In essence, scripting allows you to automate many common tasks that you would perform using the terminal in Linux. It is a very powerful skill for system administrators to learn.

First, I'm going to create a `bin` folder inside of our home folder (this will become useful later).

```bash
mkdir ~/bin
```

In that command, the tilde `~` character represents your home folder. It is one of the special folder paths that you can use on the terminal in Linux. Now, we can open that folder:

```bash
cd ~/bin
```

To begin, let's open a text file using Nano in the terminal. I'm going to use the `.sh` file extension to make it clear that this is a script, but that is not necessary on Linux.

```bash
nano script.sh
```

At the top of the file, we must define the script interpreter we would like to use. For Bash, place this line at the very top of the file:

```bash
#!/bin/bash
```

Some experienced system administrators will refer to the start of that line as a "sha-bang," which may make it easy to remember. It is actually a two-byte magic number that tells Linux what type of file it is reading, and then the rest of the line gives the path to the program that can interpret that file. This allows Linux to determine the type of the file even without checking the file extension, which is what Windows does.

Below that line, you can simply place terminal commands, one per line, that you wish to have the script perform. For example, here is a simple Hello World script:

```bash
#!/bin/bash

echo "Hello World"
exit 0
```

The echo command is pretty self-explanatory - it just prints text to the console. The final line gives the exit condition for the script. Returning zero `0` indicates that the script completed successfully. Any non-zero value is treated as an error, and can be used to diagnose failing scripts. See [Chapter 6 of the Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/exit-status.html) from TDLP for more information on exit conditions.

To run the script, save and exit the file using `CTRL+X`, then `Y`, then `ENTER`. Then, you can simply type:

```bash
./script.sh
```

and see if it works. Here, we are using the dot, or period `.`, as part of the path to the script. A single dot represents the current directory, so putting `./` in front of a file indicates that we want to run the script with that name from the current directory. At the end of the video, we'll discuss how to modify your system so you don't have to include the path to the script.

Unfortunately, it doesn't run. This is because Linux has a separate file permission to allow files and scripts to be executed. By default, most files aren't given that permission, so we have to manually add it before executing the script. To do so, type:

```bash
chmod u+x script.sh
```

This will give the owner of the file `u` the execute permission `+x`. Then, try to run it again:

```bash
./script.sh
```

It should display "Hello World" on the screen. Congratulations, you've written your first Bash script!

Now, let's take a look at a more complex script. This is one I actually wrote years ago when I first interviewed for an instructor position here at K-State:

```bash
#!/bin/bash
#batman.sh

if (( $# < 1 || $# > 1 )); then
  echo "Usage: batman.sh <name>"
  exit 1
fi

if [ "$1" = "Batman" ]; then
  echo "Hello Mr. Wayne"
elif [ "$1" = "Robin" ]; then
  echo "Welcome back Mr. Grayson"
else
  echo "Intruder alert!"
fi
exit 0
```

There is quite a bit going on in this script, so let's break it down piece by piece. First, this script includes parameters. The `$1` variable references the first parameter, and obviously `$2` would be the second, and so on. For parameter values above 9, include the number in curly braces, such as `${10}` and `${11}`.You can also access the number of parameters provided using `$#`, and the entire parameter string as `$*`.

Below that, the first if statement:

```bash
if (( $# < 1 || $# > 1 )); then
  echo "Usage: batman.sh <name>"
  exit 1
fi
```

uses double parentheses, representing arithmetic evaluation. In this case, it is checking to see if the number of parameters provided is either greater than or less than 1. If so, it will print an error message. It will also exit with a non-zero exit condition, indicating that the script encountered an error. Lastly, note that if statements are concluded with a backwards if, or "fi", indicating the end of the internal code block. In many other programming languages, curly braces (`{` and `}`) are used for this purpose.

The next if statement:

```bash
if [ "$1" = "Batman" ]; then
  echo "Hello Mr. Wayne"
elif [ "$1" = "Robin" ]; then
  echo "Welcome back Mr. Grayson"
else
  echo "Intruder alert!"
fi
```

uses square brackets for logical test comparisons. This is equivalent to using the Linux "test" command on that statement. Here, the script is checking to see if the string value of the first parameter exactly matches "Batman". If so, it will print the appropriate welcome message.

So, this simple script introduces two different methods of comparison, as well as conditional statements and parameters.

Here's another simple script to introduce a few other concepts:

```bash
#!/bin/bash
#listfiles.sh

files=`ls $* 2> /dev/null`
for afile in "$files"; do
    echo "$afile"
done
exit 0
```

The first line of the script:

```bash
files=`ls $* 2> /dev/null`
```
declares a new variable $files, and sets its value to the output of the command contained in backticks <code>`</code>. Inside of a script, any commands contained in backticks will be converted to the output of that script, which can then be stored in a variable for later use.

The next line:

```bash
for afile in "$files"; do
```

represents a "foreach" loop. It will execute the code inside of that statement once for each item in the `$files` variable. Note that when variables are declared and assigned, they don't require the dollar sign `$` in front of them, but when they are used it must be included. The loop is concluded with a "done" line at the bottom.

Finally, let's review a couple more scripts:

```bash
#!/bin/bash
#simplemenu.sh

OPTIONS="Build Run Clean Quit"

select opt in $OPTIONS; do
  if [ "$opt" = "Build" ]; then
    echo "Building project..."
  elif [ "$opt" = "Run" ]; then
    echo "Running project..."
  elif [ "$opt" = "Clean" ]; then
    echo "Cleaning project..."
  elif [ "$opt" = "Quit" ]; then
    echo "Exiting..."
    break
  else
    echo "Invalid Input"
  fi
done
exit 0
```

This script creates a simple menu with four options, stored in the `$OPTIONS` variable at the top. It then uses a "select" statement, telling the terminal to ask the user to choose one of the options provided, and then inside the select statement is a set of "if" statements determining which option the user chose. This is very similar to a "case" statement in many other programming languages. When you run this script, note that it repeats the options until it hits an option containing a "break" statement, so it is not necessary to encapsulate it in a loop.

Lastly, Bash scripts also provide the ability to read input from the user directly, instead of using command-line parameters:

```bash
#!/bin/bash
#simpleinput.sh

echo "Input your name and press [ENTER]"
read name
echo "Welcome $name!"
exit 0
```

This script uses the "read" command to read input from the user and store it in the `$name` variable. Pretty simple, right?

If you plan on writing scripts for your own use, there is one thing you can do to greatly simplify the process of using them. Notice that, currently, you must provide the full path to the script using either `./` or some other path. This is because, by default, Linux will look for commands and scripts in all of the folders contained in your `PATH `environment variable, but not the current folder. So, we must simply add the folder containing all of our scripts to the `PATH` variable.

In recent versions of Ubuntu, all you have to do is create a `bin` folder in your home folder, as we did above. Then, restart the computer and it should automatically add that folder to your path. This is because of a setting hidden in your Bash profile configuration file, usually stored in `~/.profile`. The same process works for the Windows Subsystem for Linux (WSL) version of Ubuntu as well.

You can check the current `PATH` variable using the following command:

```bash
echo $PATH
```

If you don't see your `~/bin` folder listed there after you've created it and rebooted your computer (it will usually have the full path, as in `/home/cis527/bin` or similar), you'll need to add it manually. To do this, open your Bash settings file:

```bash
nano ~/.bashrc
```
And, at the very bottom of the file, add the following line:

```
export PATH=$PATH:$HOME/bin/
```

Then, save the file, close, and reopen your terminal window. You can check your `PATH` variable once again to confirm that it worked.

Now, you can directly access any script you've created and stored in the `~/bin` folder without providing a path. So, for example, the very first script we created, stored in `~/bin/script.sh`, can now be accessed from any folder just by typing

```bash
script.sh
```

on the terminal.

This is a very brief introduction to Bash scripting. I highly recommend reading the [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/index.html) from The Linux Documentation Project (TLDP) if you'd like to learn even more about scripting.
