
# Challenge 1 cat: not the pet, but the command!

One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

```sh
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
```

`cat` will concatenate (hence the name) multiple files if provided multiple arguments. For example:

```sh
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
```

Finally, if you give no arguments at all, `cat` will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the `flag` file in your home directory (where your shell starts). Go read it with `cat`!

## Solution:

After the terminal comes up, the user needs to read from `flag` file present in home directory, this can be done using the command `cat flag`.


#### Commands run:

```sh
$ cat flag
```

## Flag: 

```
pwn.college{0do_FX4YQLvhmqoWtYWynh22UVA.QXxcTN0wyM1EzNzEzW}
```

### Notes:

- `cat` will concatenate multiple files if provided multiple arguments.
- if no arguments given at all, `cat` will read from the terminal input and output it.


# Challenge 2 catting absolute paths

In the last level, you did `cat flag` to read the flag out of your home directory! You can, of course, specify `cat`'s arguments as absolute paths:

```sh
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
```

In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with `cat` at its absolute path: `/flag`.

## Solution:

After the terminal comes up, the user needs to read from flag file present in `/flag`  
this can be done using the command `cat /flag`.

#### Commands run: 

```sh
$ cat /flag
```

## Flag: 

```
pwn.college{s8IYDA0wpawyY_N8GFWN-CPmaK2.QX5ETO0wyM1EzNzEzW}
```

### Notes:

- /flag is where the flag always lives in pwn.college, but we typically can't access that file directly.
- We can specify `cat`'s arguements as absolute path

# Challenge 3 more catting practice

You can specify all sorts of paths as arguments to commands, and we'll practice some more with `cat`. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with `cd`, so no `cat flag` for you. You must retrieve the flag by absolute path, wherever it is

## Solution:

After the terminal comes up, the user needs to read from flag file present in some directory, we can try to change directories but on doing so it says that cd is not allowed, but also reveals the absolute path of flag file.

```sh
You used 'cd'! In this level, I don't allow you to change the working directory
--- you MUST chase pass 'cat' the absolute path of where I put it on the
filesystem (which is /usr/share/giac/flag).
```

Now since the user knows the absolute path of flag file, the flag can be read using the command `cat /usr/share/giac/flag`.

#### Commands run: 

```sh
$ cd flag
$ cat /usr/share/giac/flag
```

## Flag: 

```
pwn.college{ARf9TKHLhe0CPjs-0wJ7oX2tMnh.QXwITO0wyM1EzNzEzW}
```

### Notes:

- We can specify `cat`'s arguements as absolute path.


# Challenge 4 grepping for a needle in a haystack

Sometimes, the files that you might `cat` out are too big. Luckily, we have the `grep` command to search for the contents we need! We'll learn it in this challenge.

There are many ways to `grep`, and we'll learn one way here:

```sh
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```

Invoked like this, `grep` will search the file for lines of text containing `SEARCH_STRING` and print them to the console.


In this challenge, I've put a hundred thousand lines of text into the `/challenge/data.txt` file. `grep` it for the flag!

HINT: The flag always starts with the text `pwn.college`.

## Solution:

After the terminal comes up, the user needs to read the flag present in `/challenge/data.txt` as mentioned in the challenge.  
And since the flag also starts with `pwn.college` (provided as a hint), it can be searched for using the command `grep pwn.college /challenge/data.txt`.

#### Commands run:

```sh
$ grep pwn.college /challenge/data.txt
```

## Flag: 

```
pwn.college{UiD10gqh5W-xbPcmo9z7NG-BOVh.QX3EDO0wyM1EzNzEzW}
```

### Notes:

- `grep SEARCH_STRING /path/to/file` invoked like this, `grep` will search the file for lines of text containing `SEARCH_STRING` and print them to the console.
- Many ways to use `grep`.


# Challenge 5 comparing files

When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the `diff` command becomes invaluable.

`diff` compares two files line by line and shows you exactly what's different between them. For example:

```sh
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```

The output tells us that line 2 changed (`2c2`), with `world` in the first file (`<`) being replaced by `universe` in the second file (`>`).

Sometimes, when new lines are added, you'll see something like:

```sh
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```

This tells us that after line 1 in the first file, the second file has an additional line (`1a2` means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in `/challenge`:

`/challenge/decoys_only.txt` contains 100 fake flags
`/challenge/decoys_and_real.txt` contains all 100 fake flags plus the one real flag

Use `diff` to find what's different between these files and get your flag!

## Solution:

After the terminal comes up, the user needs to find the correct flag out of a file (`/challenge/decoys_only.txt`) containing 100 fake flags and another file (`/challenge/decoys_and_real.txt`) containing those same 100 fake flags and a real flag.

This can be done using the command `diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt`.

#### Commands run:

```sh
$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
```

## Flag: 

```
pwn.college{ktDwe8HW7WESnqJ1ms1Rg4Q3yNf.01MwMDOxwyM1EzNzEzW}
```

### Notes:

- `diff` compares two files line by line and shows you exactly what's different between them.
- `1a2` means "after line 1 of file1, add line 2 of file2"


# Challenge 6 listing files

So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the `ls` command!

`ls` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

```sh
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

In this challenge, we've named `/challenge/run` with some random name! List the files in `/challenge` to find it.

## Solution:

After the terminal comes up, the user needs to invoke the `/challenge/run` program to get the flag, but the program is renamed to a random name.

The user needs to see a list of all files present in the `/challenge` directory, this can be done using the commands `cd /challenge` `ls`, this gives the outputs `5079-renamed-run-18284` and `DESCRIPTION.md`.

Since the flag cant be in `DESCRIPTION.md`, it has to be in `5079-renamed-run-18284`, this can be confirmed by reading the contents of it using the command `cat 5079-renamed-run-18284`, which gives the output 

```sh
#!/opt/pwn.college/bash

echo "Yahaha, you found me! Here is your flag:"
cat /flag
```

Now since the flag is for sure present in the file `5079-renamed-run-18284`, it can be invoked using the command `./5079-renamed-run-18284`, which gives the output-

```sh
Yahaha, you found me! Here is your flag:
pwn.college{sqSg85uctiOgTrvib7FERZ2aqa3.QX4IDO0wyM1EzNzEzW}
```


#### Commands run:

```sh
$ cd /challenge
$ ls
$ cat 5079-renamed-run-18284
$ ./5079-renamed-run-18284
```

## Flag: 

```
pwn.college{sqSg85uctiOgTrvib7FERZ2aqa3.QX4IDO0wyM1EzNzEzW}
```

### Notes:

- `ls` will list files in all the directories provided to it as arguments.
- `ls` will list all the files in the current directory if no arguments are provided.


# Challenge 7 touching files

Of course, you can also _create_ files!
There are several ways to do this, but we'll look at a simple command here.
You can create a new, blank file by _touching_ it with the `touch` command:

```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```

It's that simple!
In this level, please create two files: `/tmp/pwn` and `/tmp/college`, and run `/challenge/run` to get your flag!

## Solution:

After the terminal comes up, first the user needs to create 2 files in the `/tmp` directory named `pwn` and `college`, this can be done using the commands `cd /tmp` `touch pwn` `touch college`.

Then the user can invoke `/challenge/run` program by changing directory to root using command `cd /` and invoking the program using the command `/challenge/run`.

#### Commands run:

```sh
$ cd /tmp
$ touch pwn
$ touch college
$ ls
$ cd /
$ /challenge/run
```

## Flag: 

```
pwn.college{oTJcOoqnj1CrfyfgRyJt1JpEpnG.QXwMDO0wyM1EzNzEzW}
```

### Notes:

- `touch` command can create a new blank file


# Challenge 8 removing files

Files are all around you.
Like candy wrappers, there'll eventually be too many of them.
In this level, we'll learn to clean up!

In Linux, you **r**e**m**ove files with the `rm` command, as so:

```sh
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

Let's practice.
This challenge will create a `delete_me` file in your home directory!
Delete it, then run `/challenge/check`, which will make sure you've deleted it and then give you the flag!

## Solution:

After the terminal comes up, the user needs to remove `delete_me` file present in the home directory, this can be done using the commands `ls` `rm delete_me`.

After deleting the file, the `/challenge/check` program can be invoked using the command `/challenge/check` to give the flag.

#### Commands run:

```sh
$ ls
$ rm delete_me
$ /challenge/check
```

## Flag: 

```
pwn.college{4IcozYvzNtj_ea2i8EJTogUNIGo.QX2kDM1wyM1EzNzEzW}
```

### Notes:

- files can be deleted using the `rm` command.

















