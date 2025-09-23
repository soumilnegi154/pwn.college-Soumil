
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

Now the user knows the directory for /challenge/run program, so the directory can be changed using the second command, ```cd /usr/aarch64-linux-gnu/include/gnu```.   
Now the user can execute the program using the third command, ```/challenge/run```.

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



# Challenge 4 Position elsewhere

The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the  `cd` (change directory) command and passing a path to it as an argument, as so:

```sh
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the `~` was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

## Solution:

Similarly to challenge 3, the user needs to execute the /challenge/run program for the flag, on running the first command, `/challenge/run` it gives an error

```You are not currently in the /usr/share/build-essential directory.
Please use the `cd` utility to change directory appropriately.
```
Now the user knows the directory for /challenge/run program, so the directory can be changed using the second command, ```cd /usr/share/build-essential```.   
Now the user can execute the program using the third command, ```/challenge/run```.

#### Commands run:

```sh
$ /challenge/run
$ cd /usr/share/build-essential
$ /challenge/run
```

## Flag: 

```
pwn.college{wfLMdffw-EPMjhamN4AecsNhGZG.QX3QTN0wyM1EzNzEzW}
```

### Notes:

- ```cd``` (change directory) command can be used to navigate directories.
- the ```~``` in the shell shows the current path we are working on.


# Challenge 5 Position yet elsewhere

The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the `cd` (change directory) command and passing a path to it as an argument, as so:

```sh
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the `~` was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!
## Solution:

Similarly to challenge 4, the user needs to execute the /challenge/run program for the flag, on running the first command, `/challenge/run` it gives an error

```
You are not currently in the /etc directory.
Please use the `cd` utility to change directory appropriately.
```
Now the user knows the directory for /challenge/run program, so the directory can be changed using the second command, ```cd /etc```.  
Now the user can execute the program using the third command, ```/challenge/run```.

#### Commands run:

```sh
$ /challenge/run
$ cd /etc
$ /challenge/run
```

## Flag: 

```
pwn.college{QXo133bJOdEi_VFym2Zxsx4wEs-.QX4QTN0wyM1EzNzEzW}
```

### Notes:

- ```cd``` (change directory) command can be used to navigate directories.
- the ```~``` in the shell shows the current path we are working on.


# Challenge 6 implicit relative paths, from /

Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for relative paths.

- A relative path is any path that does not start at root (i.e., it does not start with /).
- A relative path is interpreted relative to your current working directory (cwd).
- Your cwd is the directory that your prompt is currently located at.  

This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at `/tmp/a/b/my_file`.

If my `cwd` is `/`, then a relative path to the file is `tmp/a/b/my_file`.
If my `cwd` is `/tmp`, then a relative path to the file is `a/b/my_file`.
If my `cwd` is `/tmp/a/b/c`, then a relative path to the file is `../my_file`. The `..` refers to the parent directory.

Let's try it here! You'll need to run `/challenge/run` using a relative path while having a current working directory of `/`.  For this level, I'll give you a hint. Your relative path starts with the letter `c` 😊

## Solution:

Similarly to challenge 5, the user needs to execute the /challenge/run program for the flag, on running the first command, `/challenge/run` it gives an error

```
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
```

since for this challenge, the user needs to execute the program using a relative path, first the user needs to have a current working directory of `/`.  
This can be achieved using the second command, `cd /`.  
Since the user is in the `/` working directory, the relative path to `/challenge/run` will become `challenge/run`, also a hint was given which states that our relative path starts with `c`, likely meaning it starts with "challenge".  
Now the user can execute the program using the third command, `challenge/run`.

#### Commands run:

```sh
$ /challenge/run
$ cd /
$ challenge/run
```

## Flag: 

```
pwn.college{MAfdwrJpBZ-1cMyJ7Citv3lv-ui.QX5QTN0wyM1EzNzEzW}
```

### Notes:

- A relative path is any path that does not start at root.
- A relative path is interpreted relative to your current working directory (`cwd`).
- Your cwd is the directory that your prompt is currently located at.
-  The `..` refers to the parent directory.



# Challenge 7 explicit relative paths, from /

Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: `.` and `..`. The first, `.`, refers right to the same directory, so the following absolute paths are all identical to each other:

- `/challenge`
- `/challenge/.`
- `/challenge/./././././././././`
- `/./././challenge/././`

The following relative paths are also all identical to each other:

- `challenge`
- `./challenge`
- `./././challenge`
- `challenge/.`

Of course, if your current working directory is `/`, the above relative paths are equivalent to the above absolute paths.

This challenge will get you using `.` in your relative paths. Get ready!

## Solution:

When the terminal comes up, the user needs to change the current working directory to root using the first command, `cd /`.

Then the /challenge/run program can be invoked using the relative path `./challenge/run`, which is the second command. Here the are explicitly mentioning that `challenge/run` is in the `/` directory using `.`.


#### Commands run:

```sh
$ cd /
$ ./challenge/run
```

## Flag: 

```
pwn.college{IOFr--oMoPvIY2iR7QLi5EWJHwX.QXwUTN0wyM1EzNzEzW}
```

### Notes:

- Every directory has two implicit entries that you can reference in paths: `.` and `..`.
- The first, `.` refers right to the same directory.
- `.` can be used to explicitly mention that the current directory is being used.


# Challenge 8 implicit relative path

In this level, we'll practice referring to paths using `.` a bit more. This challenge will need you to run it from the `/challenge` directory. Here, things get slightly tricky.

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:

```sh
hacker@dojo:~$ cd /challenge
hacker@dojo:/challenge$ run
```

This will not invoke /challenge/run. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:

```sh
bash: run: command not found
```

We'll explore the mechanisms behind this concept later, but in this challenge, we'll learn how to explicitly use relative paths to launch `run` in this scenario. The way to do this is to tell Linux that you explicitly want to execute a program in the current directory, using `.` like in the previous levels. Give it a try now!

## Solution:

When the terminal comes up, the user needs to change the current working directory to /challenge using the first command, `cd /challenge`. 
Now to get the flag, the user must invoke the run program. However the user cannot execute run implicitly as it will result in an error. Thus the run program needs to be explicitly mentioned using the second command, `./run`.

#### Commands run:

```sh
$ cd /challenge
$ ./run
```

## Flag: 

```
pwn.college{EqwAFwshLnLLtp4guXXPKEbnz8Y.QXxUTN0wyM1EzNzEzW}
```

### Notes:

- Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path.
- For example, invoking /challenge/run using `/challenge$ run` will result in the error `bash: run: command not found`.
- Hence we can explicitly mention that the run program is in the current working directory using `$ ./run`.



# Challenge 9 home sweet home

Every user has a home directory, typically under `/home` in the filesystem. In the dojo, you are the `hacker` user, and your home directory is `/home/hacker`. The home directory is typically where users store most of their personal files. As you make your way through pwn.college, this is where you'll store most of your solutions.

Typically, your shell session will start with your home directory as your current working directory. Consider the initial prompt:

```sh
hacker@dojo:~$
```

The `~` in this prompt is the current working directory, with `~` being shorthand for `/home/hacker`. Bash provides and uses this shorthand because, again, most of your time will be spent in your home directory. Thus, whenever bash sees `~` provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. Consider:

```sh
hacker@dojo:~$ echo LOOK: ~
LOOK: /home/hacker
hacker@dojo:~$ cd /
hacker@dojo:/$ cd ~
hacker@dojo:~$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~
hacker@dojo:~$ cd /home/hacker/asdf
hacker@dojo:~/asdf$
```

Note that the expansion of `~` is an absolute path, and only the leading `~` is expanded. This means, for example, that `~/~` will be expanded to `/home/hacker/~` rather than `/home/hacker/home/hacker`.

Fun fact: `cd` will use your home directory as the default destination:

```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ cd
hacker@dojo:~$
```

Now it's your turn to play! In this challenge, `/challenge/run` will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

- Your argument must be an absolute path.
- The path must be inside your home directory.
- Before expansion, your argument must be three characters or less.

Again, you must specify your path as an argument to `/challenge/run` as so:

```sh
hacker@dojo:~$ /challenge/run YOUR_PATH_HERE
```

## Solution:

When the terminal comes up, the user needs invoke the program `/challenge/run` and give it an arguement of a file to which it will write a copy of the flag.
Since the argument is an absolute path and inside home directory, user can use `~/`, and since the argument should be three characters or less, user can give a file which has a single character as name `f`.
Then the program writes the flag and reads it back to the user

```sh
Writing the file to /home/hacker/f!

... and reading it back to you:
```

#### Commands run:

```sh
$ /challenge/run ~/f
```

## Flag: 

```
pwn.college{k5j8rlpJU83sk1zTTNsvGd6eKVy.QXzMDO0wyM1EzNzEzW}
```

### Notes:

- `~` is shorthand for absolute path to home directory.
- Only leading `~` is expanded.
- `cd` uses home directory as default destination.








