
# Challenge 1 Matching with *

The first glob we'll learn is `*`.
When it encounters a `*` character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern.
It's easier to show you than explain:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```

Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one.
For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```

When zero files are matched, by default, the shell leaves the glob unchanged:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```

The `*` matches any part of the filename except for `/` or a leading `.` character.
For example:

```sh
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

Now, practice this yourself!
Starting from your home directory, change your directory to `/challenge`, but use globbing to keep the argument you pass to `cd` to at most four characters!
Once you're there, run `/challenge/run` for the flag!

## Solution:

After the terminal comes up, the user needs to `cd` into the `/challenge` directory using the `cd` command with argument of at most 4 characters, this can be done using matching with * through the command `cd /ch*`.

Then the user can invoke the run program to get the flag using the command `./run`.

#### Commands run:

```sh
$ cd /ch*
$ ./run
```

## Flag: 

```
pwn.college{IqswbVsUt6hgRtbZR3hFUjW2XOH.QXxIDO0wyM1EzNzEzW}
```

### Notes:

- `*` tries to replace the argument with any files that match the pattern.
- The `*` matches any part of the filename except for `/` or a leading `.` character.


# Challenge 2 Matching with ?

Next, let's learn about `?`.
When it encounters a `?` character in any argument, the shell will treat it as a **single-character** wildcard.
This works like `*`, but only matches _one_ character.
For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

Now, practice this yourself!
Starting from your home directory, change your directory to `/challenge`, but use the `?` character instead of `c` and `l` in the argument to `cd`!
Once you're there, run `/challenge/run` for the flag!

## Solution:

After the terminal comes up, the user needs to `cd` to the `/challenge` directory by passing the argument to `cd` without using `c` and `l`, this can be done using the `?` character using the command `cd /?ha??enge`.

Then the user can invoke the `run` program using the command `./run`.

#### Commands run:

```sh
$ cd /?ha??enge
$ ./run
```

## Flag: 

```
pwn.college{Y-TaC_ghSaweMP_bnUECmnGaxmu.QXyIDO0wyM1EzNzEzW}
```

### Notes:

- When shell encounters a `?` character in any argument, it will treat it as a **single-character** wildcard.


# Challenge 3 Matching with []

Next, we will cover `[]`.
The square brackets are, essentially, a limited form of `?`, in that instead of matching any character, `[]` is a wildcard for some subset of potential characters, specified within the brackets.
For example, `[pwn]` will match the character `p`, `w`, or `n`.
For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Try it here!
We've placed a bunch of files in `/challenge/files`.
Change your working directory to `/challenge/files` and run `/challenge/run` with a single argument that bracket-globs into `file_b`, `file_a`, `file_s`, and `file_h`!

## Solution:

After the terminal comes up, the user needs `cd` into `/challenge/files` using the command `cd /challenge/files` and then invoke the `/challenge/run` program using a single argument which globs the files `file_b`, `file_a`, `file_s`, and `file_h`, this can be done using the command `/challenge/run file_[absh]`.

#### Commands run:

```sh
$ cd /challenge/files
$ /challenge/run file_[absh]
```

## Flag: 

```
pwn.college{kJnWYYbhc7Juz8gnUFPLksqU7ia.QXzIDO0wyM1EzNzEzW}
```

### Notes:

- `[]` is a wildcard for some subset of potential characters, specified within the brackets.


# Challenge 4 Matching paths with []

Globbing happens on a _path_ basis, so you can expand entire paths with your globbed arguments.
For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

Now it's your turn.
Once more, we've placed a bunch of files in `/challenge/files`.
Starting from your home directory, run `/challenge/run` with a single argument that bracket-globs into the absolute paths to the `file_b`, `file_a`, `file_s`, and `file_h` files!

## Solution:

After the terminal comes up, the user needs to invoke the `/challenge/run` program using a single arguments which are the absolute paths to files `file_b`, `file_a`, `file_s`, and `file_h`. This can be done by globbing their absolute paths using the command `/challenge/run /challenge/files/file_[absh]`.

#### Commands run:

```sh
$ /challenge/run /challenge/files/file_[absh]
```

## Flag: 

```
pwn.college{gwmCCCHXdhGdoY-ff_8IYNy6Ev4.QX0IDO0wyM1EzNzEzW}
```

### Notes:

- Globbing happens on a _path_ basis, so you can expand entire paths with your globbed arguments.


# Challenge 5 Multiple Globs

So far, you've specified one glob at a time, but you can do more!
Bash supports the expansion of multiple globs in a single word.
For example:

```sh
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```

What happens above is that the shell looks for all files in `/` that start with _anything_ (including nothing), then have an `f` and an `l`, and end in _anything_ (including `ag`, which makes `flag`).

Now you try it.
We put a few happy, but diversely-named files in `/challenge/files`.
Go `cd` there and run `/challenge/run`, providing a single argument: a short (3 characters or less) globbed word with two `*` globs in it that covers every word that contains the letter `p`.

## Solution:

After the terminal comes up, the user needs to first `cd` into `/challenge/files` and then invoke program `/challenge/run` by providing a single short argument (3 characters or less) which covers every word that contains the letter `p`. 

This can be done using multiple globs by the command `/challenge/run *p*`.

#### Commands run:

```sh
$ cd /challenge/files
$ /challenge/run *p*
```

## Flag: 

```
pwn.college{c_kWHrbhH6WC_Lv2KSxSSpMCE93.0lM3kjNxwyM1EzNzEzW}
```

### Notes:

- Multiple globs can be used in the same command.


# Challenge 6 Mixing globs

Now, let's put the previous levels together!
We put a few happy, but diversely-named files in `/challenge/files`.
Go `cd` there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to `/challenge/run`) will match the files "challenging", "educational", and "pwning"!

## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` program using an argument which is 6 characters or less and includes `[]` `*` globs which match the files `challenging`, `educational` and `pwning`.

This can be done using the command `/challenge/run [cep]*`.

#### Commands run:

```sh
$  /challenge/run [cep]*
```

## Flag: 

```
pwn.college{0iYDo-0DTWHY5b61Y1gzGa7Aog8.QX1IDO0wyM1EzNzEzW}
```

### Notes:

- Multiple globs can be used in same command.


# Challenge 7 Exclusionary globbing

Sometimes, you want to filter out files in a glob!
Luckily, `[]` helps you do just this.
If the first character in the brackets is a `!` or (in newer versions of bash) a `^`, the glob inverts, and that bracket instance matches characters that _aren't_ listed.
For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Armed with this knowledge, go forth to `/challenge/files` and run `/challenge/run` with all files that don't start with `p`, `w`, or `n`!

**NOTE:** The `!` character has a different special meaning in bash when it's not the first character of a `[]` glob, so keep that in mind if things stop making sense! `^` does not have this problem, but is also not compatible with older shells.

## Solution:

After the terminal comes up, the user needs to first `cd` into `/challenge/files` using the command `cd /challenge/files`.

Then the user needs to invoke the `/challenge/run` program giving the argument of all files which dont start with `p`, `w`, or `n`, this can be done using the command `/challenge/run [!pwn]*`.


#### Commands run:

```sh
$ cd /challenge/files
$ /challenge/run [!pwn]*
```

## Flag: 

```
pwn.college{kjSd-bmdW6rBSzjv8tap5fIb5SW.QX2IDO0wyM1EzNzEzW}
```

### Notes:

- If the first character in the brackets is a `!` or (in newer versions of bash) a `^`, the glob inverts, and that bracket instance matches characters that _aren't_ listed.
- The `!` character has a different special meaning in bash when it's not the first character of a `[]` glob, so keep that in mind if things stop making sense! `^` does not have this problem, but is also not compatible with older shells.


# Challenge 8 Tab Completion

As tempting as it might be, using `*` to shorten what must be typed on the commandline can lead to mistakes.
Your glob might expand to unintended files, and you might not spot it until the `rm` command is already running!
No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is _tab completion_.
If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it.
Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into `/challenge/pwncollege`, and you can freely `cat` that file.
But you can't type the filename: we used some serious trickery to make sure that you _must_ tab-complete it.

Try it out!

```sh
hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```

When you hit that tab key, the name will expand and you'll be able to read the file.
Good luck!

## Solution:

After the terminal comes up, the user needs to `cat` the `/challenge/pwncollege` file using tab completion using the command `cat /chal<TAB>/pwn<TAB>`.

#### Commands run:

```sh
$ cat /challenge/pwncollege
```

## Flag: 

```
pwn.college{06eHWrMvIoRUtK3qTXwKdcpjuqH.0FN0EzNxwyM1EzNzEzW}
```

### Notes:

- pressing tab can autocomplete commands in shell.



# Challenge 9 Multiple Option for tab completion

Consider the following situation:

```sh
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```

There are multiple options!
What happens?

What happens varies based on the specific shell and its options.
By default `bash` will auto-expand until the first point when there are multiple options (in this case, `fl`).
When you hit tab a _second_ time, it'll print out those options.
Other shells and configurations, instead, will cycle through the options.

This challenge has a `/challenge/files` directory with a bunch of files starting with `pwncollege`.
Tab-complete from `/challenge/files/p` or so, and make your way to the flag!


## Solution:

After the terminal comes up, the user needs to read the files present in `/challenge/files` using tab completion, this can be done using the command `cat /challenge/files/p<TAB>`, this shows

```No flag in this file!```

On pressing `<TAB>` again, it shows the other files

```
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking
```
Then the user needs to read the files, till it outputs the flag. Here the flag is present in the `pwncollege-flag` file, this can be done using the command `cat /challenge/files/pwncollege-flag`.

#### Commands run:

```sh
$ cat /challenge/files/pwn
$ cat /challenge/files/pwn
$ cat /challenge/files/pwncollege-flag
```

## Flag: 

```
pwn.college{owS3uk6pQS5HoSX2PzcWJoplZAP.0lN0EzNxwyM1EzNzEzW}
```

### Notes:

- By default `bash` will auto-expand until the first point when there are multiple options (in this case, `fl`).
- When  tab is hit a _second_ time, it'll print out those options.
Other shells and configurations, instead, will cycle through the options. 


# Challenge 10 Tab Completion on Commands

Tab completion is for more than files!
You can also tab-complete commands.
This level has a command that starts with `pwncollege`, and it'll give you the flag.
Type `pwncollege` and hit the tab key to auto-complete it!

----
**NOTE:**
You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!


## Solution:

After the terminal comes up, the user needs to call the function `pwncollege-1548`, this can be done using the command `pwncollege<TAB>`.

#### Commands run:

```sh
$ pwncollege-1548
```

## Flag: 

```
pwn.college{MQ09s7P_cCSEy1qqBDXk0ddeqgQ.0VN0EzNxwyM1EzNzEzW}
```

### Notes:

- Pressing tab can also autocomplete functions.
















