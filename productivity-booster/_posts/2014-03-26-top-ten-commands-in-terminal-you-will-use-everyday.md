---
layout: post
title: Top 10 commands in terminal you will use everyday
---

In previous tutorial about [how to create todo list app in rails](http://masteruby.github.io/weekly-rails/2014/03/22/how-to-create-todo-list-app-static-pages.html)
you saw that we will use terminal with Rails most of the time.

In this tutorial you will learn top ten commands you will use everyday in
terminal.

Let's get started. First go to menu and open up: **Command Prompt** or
**PowerShell** in Windows and **Terminal** in Linux and Mac. You should see something like this:

![terminal-screen](/images/terminal-screen.png)


Ok so everything works let's begin.

## 1. cd(change directory)

To change actual working directory you use **cd** command. Type cd and
directory into you want to move.

### Move to another directory

To move into Desktop directory you will use this command:

{% highlight sh %}
$ cd Desktop
{% endhighlight %}

### Go back to previous directory

You can go back to previous directory with **cd ..**

{% highlight sh %}
$ cd ..
{% endhighlight %}

## 2.ls or dir(list directory)

**ls** command shows list of all files and directories in current working 
directory. For example to see list of files of your home directory type this
into command line in Linux and Mac.

{% highlight sh %}
$ ls
{% endhighlight %}

Type this in **Windows**

{% highlight sh %}
$ dir
{% endhighlight %}


You should see something like this:

![list-of-directories](/images/list-of-directories.png)

## 3. touch or copy con
Touch command creates empty file. For example try to create empty file in home
folder:

{% highlight sh %}
$ touch empty.txt
{% endhighlight %}

**Copy con** command serves for creating empty file in **Windows**

{% highlight sh %}
$ copy con empty.txt
{% endhighlight %}


You should see your file in home directory.

## 4. mkdir(make directory)

**mkdir** command creates empty folder. Navigate to home folder and create
folder of your choice:

{% highlight sh %}
mkdir my_folder
{% endhighlight %}

Check it out if folder has been created with **ls** or **dir**.

![create-folder](/images/create-folder.png)

You should see your folder in list. You can create any number of directories what you like. For example try create three directories:

{% highlight sh %}
mkdir folder1 folder2 folder3
{% endhighlight %}

You should see three new folders in current working directory. Let's move on.

## 5. rm(remove)

Remove command deletes folder or file.

### Remove folder
You type rm with -r and add name of the directory you want to remove:

{% highlight sh %}
$ rm -r my_folder
{% endhighlight %}


You should see that our folder has been removed. Option -r means recursive, it
removes directory with all of his content. Let's try something:

![remove-directory](/images/remove-directory.png) 

### Removing files

You can use rm for removing files too. For example create file with touch
command or copy con in Windows.

{% highlight sh %}
$ touch abc.txt
{% endhighlight %}

{% highlight sh %}
$ copy con abc.txt
{% endhighlight %}

Remove it with **rm**

{% highlight sh %}
$ rm abc.txt
{% endhighlight %}

On windows you remove files with **del** command following name of the file you want to remove.

{% highlight sh %}
$ del abc.txt
{% endhighlight %}


## 6. mv(move file or directory) 
Move command serves for renaming or moving directories.

### Rename directory or file with move

To rename your file type filename of file you want change and name of the file
you want to change it.

{% highlight sh %}
$ mv abc.txt empty.txt
{% endhighlight %}

In Windows this won't work. You have to use **ren** command to rename your
file.

Check it out with ls or dir. You should see that file abc.txt is now renamed to
empty.txt. 

![rename-file](/images/rename-file.png)

We can use mv for renaming directories too. Try something like this: Create directory **new_folder** in your home directory. Now rename it to
**dir**

{% highlight sh %}
$ mkdir new_folder
$ mv new_folder dir 
{% endhighlight %}

{% highlight sh %}
$ mkdir new_folder
$ ren new_folder dir
{% endhighlight %}

### Moving files or directory with mv

You can use mv command to move files to specific directory. Move your
**empty.txt** file to **dir**.

{% highlight sh %}
$ mv empty.txt ~/dir
$ ls
{% endhighlight %}

You can move any number of files as you want. For example create some files.
{% highlight sh %}
$ touch test1.txt test2.txt test3.txt
{% endhighlight %}

{% highlight sh %}
$ copy con test1.txt test2.txt test3.txt
{% endhighlight %}


Now move them to your folder.
{% highlight sh %}
$ mv test1.txt test2.txt test3.txt ~/dir
{% endhighlight %}



In Windows you will use **move** command instead of mv.

{% highlight sh %}
$ move test1.txt test2.txt test3.txt c:\dir
{% endhighlight %}


You don't have to type name of files to terminal, you can use regular
expressions. Try something like that:

{% highlight sh %}
$ mv *.txt ~/dir
{% endhighlight %}

{% highlight sh %}
$ move *.txt c:\dir
{% endhighlight %}

If you type **\*.txt** it means move all files to folder.

## 7. cp(copy)

Copy command takes file or group or files and copy it to specific directory. For example try copy our text files back to home directory.

{% highlight sh %}
$ cp *.txt ~
{% endhighlight %}

On Windows instead of cp you will use **copy**

{% highlight sh %}
$ copy *.txt c:\
{% endhighlight %}

Go back to your home directory. You should see our files.

## 8. sudo or runas(switch user do)

If you want to install some programs  on your Linux or Mac operating system you
will have to use sudo. Let's try to install **Openbox**, tool for creating and
editing videos in terminal.

{% highlight sh %}
$ sudo apt-get install openbox
{% endhighlight %}

Or you can use runas in Windows. Type this:
{% highlight sh %}
$ runas /user:<localmachine>\adminstrator.cmd
{% endhighlight %}

You will be prompted for your user password.

![sudo](/images/sudo.png)

Type this in and type letter Y for installation.

## 9. cat or type(concatenate)

Cat command serves for viewing of contents and concatenation of multiple files.

### Viewing content of the file with cat

Create some file and type something in it with your text editor. Then view its
content with cat.

{% highlight sh %}
$ cat test1.txt
{% endhighlight %}

On windows instead of cat you will use **type** command.

{% highlight sh %}
$ Type test1.txt
{% endhighlight %}


You should see content of your file like this.

![cat-command](/images/cat-command.png)

### Joining multiple files to one file with cat

Let's try to join our test files to one file with cat.

{% highlight sh %}
$ cat test1.txt test2.txt test3.txt > test.txt
{% endhighlight %}

## 10. clear

Clear command  remove all previous commands from screen

{% highlight sh %}
$ clear
{% endhighlight %}

On windows you will use **cls** command.

{% highlight sh %}
$ cls
{% endhighlight %}

That's all for now.

**27-03-2014 - I've updated my post after critical responses on Reddit. Now it 
contains Windows equivalent of Linux/Mac/Unix commands.**
