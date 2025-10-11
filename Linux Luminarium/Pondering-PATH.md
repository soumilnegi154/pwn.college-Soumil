
# Challenge 1 The PATH variable

It turns out that the answer to "How does the shell find `ls`?" is fairly simple.
There is a special shell variable, called `PATH`, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands.
If you blank out the variable, things go badly:

```sh
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```

Without a PATH, bash cannot find the `ls` command.

In this level, you will disrupt the operation of the `/challenge/run` program.
This program will **DELETE** the flag file using the `rm` command.
However, if it can't find the `rm` command, the flag will not be deleted, and the challenge will give it to you!
Thus, you must make it so that `/challenge/run` also can't find the `rm` command!

Keep in mind: `/challenge/run` will be a _child process_ of your shell, so you must apply the concepts you learned in [Shell Variables](https://pwn.college/linux-luminarium/variables/) to mess with its `PATH` variable!
If you don't succeed, and the flag gets deleted, you will need to restart the challenge to try again!


## Solution:

After the terminal comes up, the user needs to first clear the `rm` command from the `PATH` variable, this can be done using the command `PATH=""`.

Next the user can invoke `/challenge/run` which will not be able to delete the flag.

#### Commands run:

```sh
$ PATH=""
$ /challenge/run
```

## Flag: 

```
pwn.college{44zoREvuuYxDXFBRd3Z00tTf4pj.QX2cDM1wyM1EzNzEzW}
```

### Notes:

- There is a special shell variable called `PATH`, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands.


# Challenge 2 Setting PATH

Okay, so things break when you blank out `PATH`.
But what about doing something _useful_ with `PATH`?

Let's explore how we would, for example, add a new directory of programs to our command repertoire.
Recall that `PATH` stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:

```sh
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

If you maintain useful scripts that you want to be able to launch by bare name, this is annoying.
However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name!
For example:

```sh
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

Let's practice.
This level's `/challenge/run` will run the `win` command via its bare name, but this command exists in the `/challenge/more_commands/` directory, which is not initially in the PATH.
The `win` command is the _only_ thing that `/challenge/run` needs, so you can just overwrite `PATH` with that one directory.
Good luck!


## Solution:

After the terminal comes up, first the user needs to add the `win` command to `PATH` variable, this can be done using the command `PATH="/challenge/more_commands/"`.

Next the user can invoke `/challenge/run` to get the flag.

#### Commands run:

```sh
$ PATH="/challenge/more_commands/"
$ /challenge/run
```

## Flag: 

```
pwn.college{ILOs5MtNGG-RybiWIG-Fdrx3vut.QX1cjM1wyM1EzNzEzW}
```

### Notes:

- If we maintain useful scripts that we want to be able to launch by bare name, by adding directories to or replacing directories in this list, we can expose these programs to be launched using their bare name.


# Challenge 3 Finding Commands 

When you type the name of a command, _something_ inside one of the many directories listed in your `$PATH` variable is what actually gets executed (of course, unless the command is a builtin!).
But _which_ file, precisely?
You can find out with the aptly-named `which` command:

```sh
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```

Mirroring what the shell does when searching for commands, `which` looks at each directory in `$PATH` in order and prints the first file it finds whose name matches the argument you passed.

In this challenge, we added a `win` command somewhere in your `$PATH`, but it won't give you the flag.
Instead, it's in the same directory as a `flag` file that we made readable by you!
You must find `win` (with the `which` command), and `cat` the flag out of that directory!


## Solution:

After the terminal comes up, first the user needs to find out the directory of the `win` command, this can be done using the command `which win` which outputs
```
/challenge/paths/15265/win
```

Next the user can `cd` to `/challenge/paths/15265/` using the command `cd /challenge/paths/15265/`.

Then the user can read the flag using the command `cat flag`.

#### Commands run:

```sh
$ which win
$ cd /challenge/paths/15265/
$ cat flag
```

## Flag: 

```
pwn.college{cdKj7cuBuo6QC9lQgTErAnig83Y.01NzEzNxwyM1EzNzEzW}
```

### Notes:

- `which` command looks at each directory in `$PATH` in order and prints the first file it finds whose name matches the argument we passed.


# Challenge 4 Adding Commands

Recall our example from the previous level:

```sh
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

What we see here, of course, is the `hacker` making the shell more useful for themselves by bringing their own commands to the party.
Over time, you might amass your own elegant tools.
Let's start with `win`!

Previously, the `win` command that `/challenge/run` executed was stored in `/challenge/more_commands`.
This time, `win` does not exist!
Recall the final level of [Chaining Commands](/linux-luminarium/chaining), and make a shell script called `win`, add its location to the `PATH`, and enable `/challenge/run` to find it!

----
**Hint:**
`/challenge/run` runs as `root` and will call `win`. Thus, `win` can simply cat the flag file.
Again, the `win` command is the _only_ thing that `/challenge/run` needs, so you can just overwrite `PATH` with that one directory.
But remember, if you do that, your `win` command won't be able to find `cat`.

You have three options to avoid that:

1. Figure out where the `cat` program is on the filesystem. It _must_ be in a directory that lives in the `PATH` variable, so you can print the variable out (refer to [Shell Variables](/linux-luminarium/variables) to remember how!), and go through the directories in it (recall that the different entries are separated by `:`), find which one has `cat` in it, and invoke `cat` by its absolute path.
2. Set a `PATH` that has the old directories _plus_ a new entry for wherever you create `win`.
3. Use `read` (again, refer to [Shell Variables](/linux-luminarium/variables)) to read `/flag`. Since `read` is a builtin functionality of `bash`, it is unaffected by `PATH` shenanigans.

Now, go and `win`!


## Solution:

First the user needs to find out the directory for `cat` command, this can be done using the `which cat` command.
```
/run/dojo/bin/cat
```

Then the user needs to create a file named `win` using the command `touch win` with contents
```
/run/dojo/bin/cat /flag
```

Then the user needs to change permissions to allow root to execute `win`, this can be done using the command `chmod o+x /home/hacker/win`.

Next the user can set the `PATH` variable as `PATH="/home/hacker"`.

Now the user can invoke `/challenge/run` to get the flag.

#### Commands run:

```sh
$ which cat
$ touch win
$ chmod o+x /home/hacker/win
$ PATH="/home/hacker"
$ /challenge/run
```

## Flag: 

```
pwn.college{InfW7svAPc7n6_-5BfaMhkVCSHN.QX2cjM1wyM1EzNzEzW}
```

### Notes:

- different entries are separated by `:` in `PATH` variable.


# Challenge 5 Hijacking Commands

Armed with your knowledge, you can now carry out some shenanigans.
This challenge is almost the same as the first challenge in this module.
Again, this challenge will delete the flag using the `rm` command.
But unlike before, it will _not_ print anything out for you.

How can you solve this?
You know that `rm` is searched for in the directories listed in the `PATH` variable.
You have experience creating the `win` command when the previous challenge needed it.
What else can you create?


## Solution:

Since the `rm` command in `/challenge/run` will delete the flag, we can create another command named `rm` which reads the flag and replace it in the `PATH` variable.

First the user needs to find the location and names of `cat` and `rm`.
```
/run/dojo/bin/cat
/run/dojo/bin/rm
```

Then the user needs to create a file named `rm` with contents
```
/run/dojo/bin/cat /flag
```

Then the user needs to change its permissions so that `root` can execute it using the command `chmod o+x /home/hacker/win`.

Next the user needs to set the `PATH` variable as `PATH="/home/hacker"`

Now the user can invoke `/challenge/run` and get the flag.

#### Commands run:

```sh
$ which rm
$ which cat
$ chmod o+x /home/hacker/win
$ PATH="/home/hacker"
$ /challenge/run
```

## Flag: 

```
pwn.college{0gHekV7JGO3qS3ABz_9ptywbDfl.QX3cjM1wyM1EzNzEzW}
```

### Notes:

- We can create commands with same name to hijack commands.
