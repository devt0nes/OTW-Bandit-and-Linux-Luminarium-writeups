# Pondering Paths

## The Root

### Challenge

Alright, so the filesystem starts at `/`. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, _flags_. In this level, we've added a program right in `/`, called `pwn`, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from `/`, so the path would be `/pwn`. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the `pwn` program using its absolute path, and Capture that Flag! Good luck!  

### Solution  

As we start by default in the root directory `/` and `pwn` lies right in here, to run the program all we have to do is use its absolute path i.e. `/pwn` to get the flag.
```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{cKdJv3b9l1t54zgtiotjQad3a80.QX4cTO0wiNyAjMwEzW}
```

### Flag
> pwn.college{cKdJv3b9l1t54zgtiotjQad3a80.QX4cTO0wiNyAjMwEzW}

## Program and Absolute Paths

### Challenge

Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the `challenge` directory and the `challenge` directory is, in turn, right in the root directory (`/`). The path to the challenge the directory is, thus, `/challenge`. The name of the challenge program in this level is `run`, and it lives in the `/challenge` directory. Thus, the path to the `run` challenge program is `/challenge/run`.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the `run` file that is in the `challenge` directory that is, in turn, in the `/` directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

### Solution

The `run` program resides within the `challenge` directory, so to execute it all we have to do is put its absolute path `/challenge/run` into the terminal to get the flag.
```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{IYOMSsnGjTQFA8WWmqpBzXqVuaX.QX1QTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{IYOMSsnGjTQFA8WWmqpBzXqVuaX.QX1QTN0wiNyAjMwEzW}

## Position thy self

### Challenge

The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the `cd` (`c`hange `d`irectory) command and passing a path to it as an argument, as so:

    hacker@dojo:~$ cd /some/new/directory
    hacker@dojo:/some/new/directory$ cd /some/new/directory
    

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the `~` was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the `/challenge/run` program from a specific path (which it will tell you). You'll need to `cd` to that directory before rerunning the challenge program. Good luck!  

### Solution  

As given in the problem, we first need to run `/challenge/run` to get the path of the directory where the challenge actually exists.
```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /sys/kernel directory.
Please use the `cd` utility to change directory appropriately.
```
As we're told the location of the challenge is actualy `/sys/kernel`, we can navigate into there using the `cd` command as `cd /sys/kernel`, followed by running `/challenge/run` (now in the required directory) to get the flag.
```
hacker@paths~position-thy-self:~$ cd /sys/kernel
hacker@paths~position-thy-self:/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{EYN0ODKiCIsiFsV1oThIfzIwf1b.QX2QTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{EYN0ODKiCIsiFsV1oThIfzIwf1b.QX2QTN0wiNyAjMwEzW}

## Position elsewhere

### Challenge

[Same as **Position thy self**]

### Solution

Same method as for **Position thy self**, with only the required directory `/proc/343` being different.
```
hacker@paths~position-elsewhere:~$ cd /proc/343
hacker@paths~position-elsewhere:/proc/343$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{0FZhnyd4bjcuSZ-JaQMLfQIo8mu.QX3QTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{0FZhnyd4bjcuSZ-JaQMLfQIo8mu.QX3QTN0wiNyAjMwEzW}

## Position yet elsewhere

### Challenge

[Same question statement as **Position thy self**]

### Solution

Same method as for **Position thy self**, with only the required directory `/var` being different.
```
hacker@paths~position-yet-elsewhere:~$ cd /var
hacker@paths~position-yet-elsewhere:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{4qGfBse5pXylwSKAG1IrlqWiofl.QX4QTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{4qGfBse5pXylwSKAG1IrlqWiofl.QX4QTN0wiNyAjMwEzW}

## implicit relative paths, from /

### Challenge

Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for **relative** paths.

*   A relative path is any path that does not start at root (i.e., it does not start with `/`).
*   A relative path is interpreted **relative** to your **c**urrent **w**orking **d**irectory (`cwd`).
*   Your `cwd` is the directory that your prompt is currently located at.

This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at `/tmp/a/b/my_file`.

*   If my `cwd` is `/`, then a relative path to the file is `tmp/a/b/my_file`.
*   If my `cwd` is `/tmp`, then a relative path to the file is `a/b/my_file`.
*   If my `cwd` is `/tmp/a/b/c`, then a relative path to the file is `../my_file`. The `..` refers to the parent directory.

Let's try it here! You'll need to run `/challenge/run` using a relative path while having a current working directory of `/`. For this level, I'll give you a hint. Your relative path starts with the letter `c` 😊

### Solution

First we must make the root directory `/` our `cwd` using `cd /`. Then, as the relative path of `/challenge/run` from `/` would simply be `challenge/run`, we enter it into the terminal to get the flag.
```
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{ojwkkUx57rIKJbZwVUtvvmekiyR.QX5QTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{ojwkkUx57rIKJbZwVUtvvmekiyR.QX5QTN0wiNyAjMwEzW}

## explicit relative paths, from /

### Challenge

Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: `.` and `..`. The first, `.`, refers right to the same directory, so the following absolute paths are all identical to each other:

*   `/challenge`
*   `/challenge/.`
*   `/challenge/./././././././././`
*   `/./././challenge/././`

The following relative paths are also all identical to each other:

*   `challenge`
*   `./challenge`
*   `./././challenge`
*   `challenge/.`

Of course, if your current working directory is `/`, the above relative paths are equivalent to the above absolute paths.

This challenge will get you using `.` in your relative paths. Get ready!

## Solution

Again, first make `/` the `cwd` using `cd /`. Then, as we are supposed to use `.` (referring to the same/current directory) in our relative path `challenge/run`, enter `./challenge/run` or any other similar relative path (having `./` in the start) to get the flag.
```
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/./run
Correct!!!
./challenge/./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{EIS1DhLbpDFgcBuLnCoJEPE-uiN.QXwUTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{EIS1DhLbpDFgcBuLnCoJEPE-uiN.QXwUTN0wiNyAjMwEzW}

## implicit relative path

### Challenge

In this level, we'll practice refering to paths using `.` a bit more. This challenge will need you to run it from the `/challenge` directory. Here, things get slightly tricky.

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:

    hacker@dojo:~$ cd /challenge
    hacker@dojo:/challenge$ run
    

This will _not_ invoke /challenge/run. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:

    bash: run: command not found
    

We'll explore the mechanisms behind this concept later, but in this challenge, will learn how to explicitly use relative paths to launch `run` in this scenario. The way to do this is to _tell_ Linux that you explicitly want to execute a program in the current directory, using `.` like in the previous levels. Give it a try now!

### Solution

First to navigate into `/challenge`, we enter the command `cd /challenge`. Then to invoke `run` using its relative path we need to specify the `/challenge` directory using `/.`. This will give the flag.
```
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{0-trzsIcTrpV7RBwUQdJoruxBIs.QXxUTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{0-trzsIcTrpV7RBwUQdJoruxBIs.QXxUTN0wiNyAjMwEzW}

## home sweet home

### Challenge

Every user has a _home directory_, typically under `/home` in the filesystem. In the dojo, you are the `hacker` user, and your home directory is `/home/hacker`. The home directory is typically where users store most of their personal files. As you make your way through pwn.college, this is where you'll store most of your solutions.

Typically, your shell session will start with your home directory as your current working directory. Consider the initial prompt:

    hacker@dojo:~$
    

The `~` in this prompt is the current working directory, with `~` being shorthand for `/home/hacker`. Bash provides and uses this shorthand because, again, most of your time will be spent in your home directory. Thus, whenever bash sees `~` provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. Consider:

    hacker@dojo:~$ echo LOOK: ~
    LOOK: /home/hacker
    hacker@dojo:~$ cd /
    hacker@dojo:/$ cd ~
    hacker@dojo:~$ cd ~/asdf
    hacker@dojo:~/asdf$ cd ~/asdf
    hacker@dojo:~/asdf$ cd ~
    hacker@dojo:~$ cd /home/hacker/asdf
    hacker@dojo:~/asdf$
    

Note that the expansion of `~` is an _absolute_ path, and only the leading `~` is expanded. This means, for example, that `~/~` will be expanded to `/home/hacker/~` rather than `/home/hacker/home/hacker`.

Fun fact: `cd` will use your home directory as the default destination:

    hacker@dojo:~$ cd /tmp
    hacker@dojo:/tmp$ cd
    hacker@dojo:~$
    

Now it's your turn to play! In this challenge, `/challenge/run` will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

1.  Your argument must be an absolute path.
2.  The path must be inside your home directory.
3.  Before expansion, your argument must be three characters or less.

### Solution

For the arguemnt of the command `/challenge/run`, we require an absolute path within the home directory that also isn't greater than three characters as a whole. Seeing as the absolute path of any file in the home directory will start as `~/`, its name must only be one character long, e.g. `~/w`. Thus, the command will be `/challenge/run ~/w`, which will write the flag into the file `w`.
```
hacker@paths~home-sweet-home:~$ /challenge/run ~/w
Writing the file to /home/hacker/w!
... and reading it back to you:
pwn.college{ER4KfAny-19hnW_LDUrwq6PtdzR.QXzMDO0wiNyAjMwEzW}
```
After writing we can also check the flag from the file using the `cat` command (here, `cat w` or `cat ~/w`).

### Flag
> pwn.college{ER4KfAny-19hnW_LDUrwq6PtdzR.QXzMDO0wiNyAjMwEzW}