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
* [Gitignore Documentation](https://git-scm.com/docs/gitignore) from Git Documentation
* [Gitignore Templates](https://github.com/github/gitignore) from GitHub

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
cd ~/git-test
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

So, to perform this process on the two files currently in our directory, we'll do this command to stage them:

```bash
git add file1.txt file2.txt
```

Once they are staged, we can check the status to make sure they are ready to commit:

```bash
git status
```

If everything looks correct, we can commit those changes:

```bash
git commit -m "First Commit"
```

The `-m` flag on the `git commit` command allows us to specify a commit message on the command line. If you omit that option, you'll be taken to your system's default text editor, usually Nano or Vim, and be able to write a commit message there. Once you are done, just save and close the file as you normally would, and the `git` command will proceed to commit the changes.

Finally, once you have committed your changes, you can review the status of your repository again:

```bash
git status
```

You can also review the Git log to see a log of your commits:

```bash
git log
```

Now that we've created a Git repository and added our first commit, let's talk about remotes. A remote in Git is a remote copy of a repository, which can be used as a backup for yourself, or as a way to share a repository with other developers. Most commonly, your remote will be an online service such as GitHub or GitLab, but there are many others as well. For this example, I'll show you how to work with the GitLab instance hosted by K-State CS. The instructions are very similar for GitHub as well.

First, you'll need to navigate to [http://gitlab.cs.ksu.edu](http://gitlab.cs.ksu.edu) and sign-in with your K-State CS username and password. Once you've logged in, go to your account settings, and look for the **SSH Keys** option. In order to authenticate your system with GitLab, you'll need to create an SSH key and copy-paste the public key here. See the SSH video in the Extras module for detailed instructions on creating those keys. I'll perform the steps quickly for this example as well. Once you are done, you can click the logo in the upper-left to go back to the dashboard.

On the dashboard, you can click the **New Project** button to create a new project. To make it simple, I'm going to give it the same name as my folder, `git-test`. I can also give it a description, and I'll need to set the visibility level for this project. I'm going to use the **Private** option for now, so I'll be the only one able to see this project.

Once your project is created, it will give you some handy instructions for using it. We're going to do the last option, which is to use an existing Git repository. So, at any time in the future, you can easily follow those instructions to get everything set up correctly.

Back on the terminal, we'll need to add a remote to our Git repository. The command for this is:

```bash
git remote add origin <url>
```

Then, we'll need to push our repository to the remote server. Since we don't have any locally created branches or tags, we can just use this command:

```bash
git push -u origin master
```

If you have already created branches or tags in this repository, you can push them to the remote server using these commands:

```bash
git push -u origin --all
git push -u origin --tags
```

There you go! Your Git repository is set to be tracked by a remote server. If you open the GitLab page, you can now see your files here as well. You can now use that remote server to share this repository across multiple computers, or even with multiple developers. For example, let's see how we could get a copy of this repository on another computer, make changes, and share those changes with both systems.

First, on the other computer, you'll need to also create an SSH key and add it to your account on GitLab. I've already done so for this system.

Next, we'll need to get a copy of the repository from the remote server using this command:

```bash
git clone <url>
```

That will create a copy of the repository in a subfolder of the current folder. Now, we can open that folder and edit a file:

```bash
cd git-test
echo "Some Changes" >> file1.txt
```

As you make edits, you can see all of the changes since your last commit using a couple of commands. First:

```bash
git status
```

will give you a list of the files changed, created, or deleted since the last commit. You can see the details of the changes using:


```bash
git diff HEAD
```

which will show you all of the changed files and those changes since the last commit.

Now, we can stage any changes using:

```bash
git add .
```

which will automatically add any changed, added, or removed files to the index. This command is very handy if you want to add all changed files to the repository at once, since you don't have to explicitly list each one. Then, we can commit those changes using:

```bash
git commit -m "Modified file1.txt"
```

and finally, we can upload those changes to the remote server using:

```bash
git push
```

If we view the project on GitLab, we can see the changes there as well. Finally, on our original computer, we can use this command to download those changes:

```bash
git pull
```

If you have made changes on both systems, it is a good idea to always commit those changes to the local repository before trying to use `git pull` to download remote changes. As long as the changes don't conflict with each other, you'll be in good shape. If they conflict, you'll have to fix them manually. I'll discuss how to do that a bit later as we deal with branching and merging.

Another major feature of Git is the ability to create branches in the repository. For example, you might have a really great idea for a new feature as you are working on a project. However, you are worried that it might not work, and you don't want to lose the progress you have so far. So, you can create a branch of the project and develop your feature there. If it works, you can merge those changes back into the master branch of your project. If it doesn't, you can just switch back to the master branch without merging, and all of your original code is just as you left it.

To create and switch to a new branch, you can use these commands:

```bash
git branch <branch_name>
git checkout <branch_name>
```

It should tell you that you switched to your new branch. You can also run

```bash
git status
```

at any time to see what branch you are currently on. Now, let's make some changes:

```bash
echo "File 12" > file1.txt
echo "More Changes" >> file2.txt
```

Here, you'll note that I am overwriting the contents in `file1.txt` since I only used one `>` symbol, while I am adding a third line of content to `file2.txt` since I used `>>` to append to that file. You can always see the changes using:

```bash
git diff HEAD
```

Now, let's commit those changes:

```bash
git add .
git commit -m "Branch Commit"
git push -u origin <branch_name>
```

Notice that the first time you push to a new branch, you'll need to provide the `-u <branch_name>` option to tell Git which branch to use. Once you've done that the first time, you can just use `git push` in the future.

Now, let's switch back to the master branch and make some changes there as well:

```bash
git checkout master
echo "File 13" > file1.txt
git add .
git commit -m "Master Commit"
git push
```

At this point, let's try to merge the changes from my new branch back into the master branch. To merge branches, you'll need to switch to the destination branch, which I've already done, then use this command:

```bash
git merge <branch_name>
```

If none of the changes cause a conflict, it should tell you that it was able to merge the branches successfully. However, in this case, we have created a conflict. This is because we have modified `file1.txt` in both branches, and Git cannot determine how to merge them together in the best way. While Git is very smart and able to merge modified files in many cases, it isn't able to do it when the same lines are changed in both files and it can't determine which option is correct. So, it will require you to intervene and make the changes.

So, let's open the file:

```bash
nano file1.txt
```

Here, you should see content similar to this

```diff
<<<<<<< HEAD
File 13
=======
File 12
>>>>>>> new_branch
```

The first section, above the line of equals signs `=`, is the content that is in the destination branch, or the branch that you are merging into. The section below that shows the content in the incoming branch. To resolve the conflict, you'll need to delete all of the lines except the ones you want to keep. So, I'll keep the change in the incoming branch in this case:

```
File 12
```

and then I'll save and close the file using <kbd>CTRL</kbd>+<kbd>X</kbd>, then <kbd>Y</kbd>, then <kbd>ENTER</kbd>. Once I've resolved all of the conflicts, I'll need to commit them:

```bash
git add .
git commit -m "Resolve Merge Conflicts"
git push
```

Congratulations! You've now dealt with branching and merging in Git.

Finally, there are a couple of handy features of Git that I'd like to point out. First is the tagging system. At any time, you can create a tag based on a commit. This is typically used to mark a particular version or release of a program, or maybe even an assignment in a course. It makes it easy to find that particular commit later on, in case you need to jump back to it. To create and push a tag, you can do the following commands:

```bash
git tag -a <tag_name> -m <message>
git push
```

You can see the tags on GitLab too. It is a very handy feature when working with large projects.

Also, if you have some files that you don't want Git to track, you can use a `.gitignore` file. It is simply a list of patterns that specify files, folders, paths, file extensions, and more that should be left out of Git's index. I encourage you to read the documentation for this feature, which is linked in the resources section below the video. There are also some great sample `.gitignore` templates from GitHub linked there as well.

I hope this video has given you a brief introduction of Git and how you could use it as a system administrator. If you'd like to learn even more about Git, I encourage you to review the links in the resources section below this video for even more information and examples of how you can use Git.
