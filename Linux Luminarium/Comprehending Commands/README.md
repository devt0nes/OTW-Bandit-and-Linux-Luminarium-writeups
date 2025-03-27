# Comprehending Commands

## cat: not the pet, but the command!

### Challenge

One of the most critical Linux commands is `cat`. `cat` is most often used for reading out files, like so:

    hacker@dojo:~$ cat /challenge/DESCRIPTION.md
    One of the most critical Linux commands is `cat`.
    `cat` is most often used for reading out files, like so:
    

`cat` will con**cat**enate (hence the name) multiple files if provided multiple arguments. For example:

    hacker@dojo:~$ cat myfile
    This is my file!
    hacker@dojo:~$ cat yourfile
    This is your file!
    hacker@dojo:~$ cat myfile yourfile
    This is my file!
    This is your file!
    hacker@dojo:~$ cat myfile yourfile myfile
    This is my file!
    This is your file!
    This is my file!
    

Finally, if you give no arguments at all, `cat` will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the `flag` file in your home directory (where your shell starts). Go read it with `cat`!

### Solution

All that needs to be done here is use the `cat` command with the argument `flag` which will read the 'flag' file and give it to us.
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{kc1m_DbNHCeXAQrgyar1VWX9y8Z.QXxcTN0wiNyAjMwEzW}
```

### Flag
> pwn.college{kc1m_DbNHCeXAQrgyar1VWX9y8Z.QXxcTN0wiNyAjMwEzW}

## catting absolute paths

### Challenge

In the last level, you did `cat flag` to read the flag out of your home directory! You can, of course, specify `cat`'s arguments as absolute paths:

    hacker@dojo:~$ cat /challenge/DESCRIPTION.md
    In the last level, you did `cat flag` to read the flag out of your home directory!
    You can, of course, specify `cat`'s arguments as absolute paths:
    ...
    

In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with `cat` at its absolute path: `/flag`.

* * *

**FUN FACT:** `/flag` is where the flag _always_ lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

### Solution

Running the `cat` command with the absolute path of the 'flag' file `/flag` will give us the flag.
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{gMu8eNoIvNPf-cafRU24P88Gjv0.QX5ETO0wiNyAjMwEzW}
```

### Flag
> pwn.college{gMu8eNoIvNPf-cafRU24P88Gjv0.QX5ETO0wiNyAjMwEzW}

## more catting practice

### Challenge

You can specify all sorts of paths as arguments to commands, and we'll practice some more with `cat`. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with `cd`, so no `cat flag` for you. You must retrieve the flag by absolute path, wherever it is.

### Solution

Here, we would need to look through each directory one by one till we find the `flag` file, but one workaround is that using `cd` (despite it not working) will give us the absolute path of the file.  
We can then use that along with `cat` to read the file and get the flag.
```
hacker@commands~more-catting-practice:~$ cd
You used 'cd'! In this level, I don't allow you to change the working directory 
--- you MUST chase pass 'cat' the absolute path of where I put it on the 
filesystem (which is /usr/lib/openssh/flag).
hacker@commands~more-catting-practice:~$ cat /usr/lib/openssh/flag
pwn.college{I2Brfydwo9reRoz-3x0iZK_ebhH.QXwITO0wiNyAjMwEzW}
```

### Flag
> pwn.college{I2Brfydwo9reRoz-3x0iZK_ebhH.QXwITO0wiNyAjMwEzW}

## grepping for a needle in a haystack

### Challenge

Sometimes, the files that you might `cat` out are too big. Luckily, we have the `grep` command to search for the contents we need! We'll learn it in this challenge.

There are many ways to `grep`, and we'll learn on way here:

    hacker@dojo:~$ grep SEARCH_STRING /path/to/file
    

Invoked like this, `grep` will search the file for lines of text containing `SEARCH_STRING` and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the `/challenge/data.txt` file. Grep it for the flag!

HINT: The flag always starts with the text `pwn.college`.  

### Solution

As given, we need to search for the flag within the `data.txt` file using `grep`, for which the command will be `grep pwn.college /challenge/data.txt`. Doing so will find the flag from amongst all the useless data.  
```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{I5WbYMSxrL5JUk8LA4fdq8jstmI.QX3EDO0wiNyAjMwEzW}
```

### Flag
> pwn.college{I5WbYMSxrL5JUk8LA4fdq8jstmI.QX3EDO0wiNyAjMwEzW}

## listing files

### Challenge

So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to **l**i**s**t their contents using the `ls` command!

`ls` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

    hacker@dojo:~$ ls /challenge
    run
    hacker@dojo:~$ ls
    Desktop    Downloads  Pictures  Templates
    Documents  Music      Public    Videos
    hacker@dojo:~$ ls /home/hacker
    Desktop    Downloads  Pictures  Templates
    Documents  Music      Public    Videos
    hacker@dojo:~$
    

In this challenge, we've named `/challenge/run` with some random name! List the files in `/challenge` to find it.  

### Solution

To find the required file, we need to list the all those present within `/challenge` using `ls` as `ls /challenge`. Doing so shows that there's a file within that directory named `2228-renamed-run-3332`, which we execute to get the flag.  
```
hacker@commands~listing-files:~$ ls /challenge
2228-renamed-run-3332  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/2228-renamed-run-3332
Yahaha, you found me! Here is your flag:
pwn.college{A_G36WqVMSVPrH2RLFcnwX_vdUD.QX4IDO0wiNyAjMwEzW}
```

### Flag
> pwn.college{A_G36WqVMSVPrH2RLFcnwX_vdUD.QX4IDO0wiNyAjMwEzW}

## touching files

### Challenge

Of course, _you_ can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by _touching_ it with the `touch` command:

    hacker@dojo:~$ cd /tmp
    hacker@dojo:/tmp$ ls
    hacker@dojo:/tmp$ touch pwnfile
    hacker@dojo:/tmp$ ls
    pwnfile
    hacker@dojo:/tmp$
    

It's that simple! In this level, please create two files: `/tmp/pwn` and `/tmp/college`, and run `/challenge/run` to get your flag!  

### Solution  

Creating both the files can be done by using the `touch` command with the files required as arguments, as `touch /tmp/pwn` and `touch /tmp/college`. After this, using `/challenge/run` will give the flag.  
```
hacker@commands~touching-files:~$ touch /tmp/pwn
hacker@commands~touching-files:~$ touch /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{EDFOk_p2roQmWB83bbSMPmtlYYt.QXwMDO0wiNyAjMwEzW}
```

### Flag
> pwn.college{EDFOk_p2roQmWB83bbSMPmtlYYt.QXwMDO0wiNyAjMwEzW}

## removing files

### Challenge

Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you **r**e**m**ove files with the `rm` command, as so:

    hacker@dojo:~$ touch PWN
    hacker@dojo:~$ touch COLLEGE
    hacker@dojo:~$ ls
    COLLEGE     PWN
    hacker@dojo:~$ rm PWN
    hacker@dojo:~$ ls
    COLLEGE
    hacker@dojo:~$
    

Let's practice. This challenge will create a `delete_me` file in your home directory! Delete it, then run `/challenge/check`, which will make sure you've deleted it and then give you the flag!  

### Solution

Using `ls` we can see the `delete_me` file in the home directory. Removing it using `rm` as `rm delete_me` and then running `/challenge/check` will give us the flag.  
```
hacker@commands~removing-files:~$ ls
Desktop  delete_me  r  w
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{8dps9dG-GV8B409P2dCoSA2rxbp.QX2kDM1wiNyAjMwEzW}
```

### Flag
> pwn.college{8dps9dG-GV8B409P2dCoSA2rxbp.QX2kDM1wiNyAjMwEzW}

## hidden files

### Challenge

Interestingly, `ls` doesn't list _all_ the files by default. Linux has a convention where files that start with a `.` don't show up by default in `ls` and in a few other contexts. To view them with `ls`, you need to invoke `ls` with the `-a` flag, as so:

    hacker@dojo:~$ touch pwn
    hacker@dojo:~$ touch .college
    hacker@dojo:~$ ls
    pwn
    hacker@dojo:~$ ls -a
    .college	pwn
    hacker@dojo:~$
    

Now, it's your turn! Go find the flag, hidden as a dot-prepended file in `/`.  

### Solution

To see all the files in `/` including the hidden ones, we must use the `-a` attribute along with `ls`, as `ls -a /` (simply using `ls /` doesn't show any relevant files). Doing so shows us a hidden file named `.flag-206981888832015`, which we can read using `cat .flag-206981888832015`.  
```
hacker@commands~hidden-files:~$ ls /
bin  boot  challenge  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@commands~hidden-files:~$ ls -a /
.  ..  .dockerenv  .flag-206981888832015  bin  boot  challenge  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@commands~hidden-files:~$ cat /.flag-206981888832015
pwn.college{kcozaNuirCF0QgMm4H8EYwhNsVp.QXwUDO0wiNyAjMwEzW}
```

### Flag
> pwn.college{kcozaNuirCF0QgMm4H8EYwhNsVp.QXwUDO0wiNyAjMwEzW}

## An Epic Filesystem Quest