---
title: "Git"
weight: 35
pre: "7. "
---

{{< youtube >}}

#### Resources

* [Resources to Learn Git](https://try.github.io/) from GitHub
* [Git Tutorial](https://git-scm.com/docs/gittutorial) from Git Documentation
* [Git Homepage](https://git-scm.com/)
* [Become a Git Guru](https://www.atlassian.com/git/tutorials) from Atlassian
* [Git Tutorial](https://www.tutorialspoint.com/git/) from Tutorialspoint
* [Git Tutorial Slides](https://russfeld.me/presentations/2016gittutorial/presentation.html#/learning) by Russell Feldhausen
* [GitHub Desktop](https://desktop.github.com/) from GitHub
* [Git Kraken](https://www.gitkraken.com/) from Axosoft

#### Video Transcript

This video provides a brief introduction to the Git source control program used by many system administrators. While this video is not intended to provide a full introduction to Git as a programmer would use it, it should serve as a quick introduction to the ways that system administrators might come across Git in their workloads.

For this example, I'll be working with the command-line `git` program. There are many graphical programs that can be used to interact with Git as well, such as GitHub Desktop and Git Krakken

If you haven't already, you'll need to install the Git command-line tool. You can do so using `apt`:

```bash
sudo apt update
sudo apt install git
```

Also, if you have not used Git on this system, you'll want to configure your name and email address used when you create commits:

```bash
git config --global user.name "Your Name"
git config --global user.email username@emailprovider.tld
```

Now, let's create a new Git repository on our computer. To do that, I'm going to create a new folder called `git-test` and add a couple of files to it:

```bash
mkdir ~/git-test
chdir ~/git-test
echo "File 1" > file1.txt
echo "File 2" > file2.txt
```

Next, let's initialize an empty Git repository in this folder. This is the first step to adding an existing folder to Git. You can also use this command in an empty folder before you begin adding content.

```bash
git init
```

Once you've done that command, let's look at the directory and show all the hidden files:

```bash
ls -al
```

As you can see, there is now a folder `.git` in this directory. That folder contains the information for this Git repository, including all of the history and changes. **DO NOT MODIFY OR DELETE THIS FOLDER!** If you change this folder, it may break your Git repository.

To see the status of a Git repository, you can use the `git status` command:

```bash
git status
```

Here you'll see that there are two files that are not included in the repository, which are the files we added earlier. To add a file to a Git repository, there are three steps. First, you must create or modify the file on the filesystem inside a git repository, which will cause Git to see the file as modified or "dirty." Then, any changes you'd like to add to the Git repository will need to be "staged" using the `git add` command. Finally, those changes which are staged are "committed" using the `git commit` command.

So, to perform this process on the two files currently in our directory, we'll do these commands to stage them:

```bash
git add file1.txt file2.txt
```

Once they are staged, we can check the status to make sure they are ready to commit:

```bash
git status
```

If everything looks correct, we can commit those changes:

```bash
git commit -m "First Commit Message"
```

The `-m` flag on the `git commit` command allows us to specify a commit message on the command line. If you omit that option, you'll be taken to your system's default text editor, usually Nano or Vim, and be able to write a commit message there. Once you are done, just save and close the file as you normally would, and the `git command` will proceed to commit the changes.

Finally, once you have committed your changes, you can review the status of your repository again:

```bash
git status
```

You can also review the Git log to see a log of your commits:

```bash
git log
```












I hope this video has given you a brief introduction of Git and how you could use it as a system administrator. If you'd like to learn even more about Git, I encourage you to review the links in the resources section below this video for even more information and examples of how you can use Git.
