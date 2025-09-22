
# Challenge 1 The Root

Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!


## Solution:

After the terminal comes up, the user needs to execute the pwn program using its absolute path, then it outputs the flag on the shell.

#### Commands run: 

```sh
$ /pwn
```

## Flag: 

```
pwn.college{AUKpVn2zQGHKtbmOLoEw_TsEPOA.QX4cTO0wyM1EzNzEzW}
```

### Notes:

- This style of path, one that starts with the root directory, is referred to as an "absolute path".
- The root of the filesystem is a directory, and every directory can contain other directories and files.
- You refer to files and directories by their path. A path from the root of the filesystem starts with / (that is, the root of the filesystem), and describes the set of directories that must be descended into to find the file. Every piece of the path is demarcated with another ```/```.



# Challenge 2 Program and Absolute Paths

Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

## Solution:

After the terminal comes up, the user needs to execute the run challenge file (run) in the /challenge directory using its absolute path, then it outputs the flag on the shell.

#### Commands run:

```sh
$ /challenge/run
```

## Flag: 

```
pwn.college{E1YG4d90DOMkmujWei9H7rz7eA7.QX1QTN0wyM1EzNzEzW}
```

### Notes:

- Any program can be executed using its absolute path.
- The Linux filesystem is a "tree".



# Challenge 3 Position thy self

The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the ```cd``` (change directory) command and passing a path to it as an argument, as so:

```sh
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ```~``` was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the ```/challenge/run``` program from a specific path (which it will tell you). You'll need to ```cd``` to that directory before rerunning the challenge program. Good luck!

## Solution:
After the terminal comes up, the user needs to execute /challenge/run file for the flag, on running the first command, ```/challenge/run``` it gives an error

```
You are not currently in the /usr/aarch64-linux-gnu/include/gnu directory.
Please use the `cd` utility to change directory appropriately
```

Now the user knows the directory for /challenge/run program, so the directory can be changed using the second command, ```cd /usr/aarch64-linux-gnu/include/gnu```  
Now we can execute the program using the third command, ```/challenge/run```.

#### Commands run:

```sh
$ /challenge/run
$ cd /usr/aarch64-linux-gnu/include/gnu
$ /challenge/run
```

## Flag: 

```
pwn.college{8A27D39WkOF-KZ1v0Gxgmgwf0IJ.QX2QTN0wyM1EzNzEzW}
```

### Notes:

- ```cd``` (change directory) command can be used to navigate directories.
- the ```~``` in the shell shows the current path we are working on.


