
# Challenge 1 Redirecting Output

First, let's look at redirecting stdout to files.
You can accomplish this with the `>` character, as so:

```sh
hacker@dojo:~$ echo hi > asdf
```

This will redirect the output of `echo hi` (which will be `hi`) to the file `asdf`.
You can then use a program such as `cat` to output this file:

```sh
hacker@dojo:~$ cat asdf
hi
```

In this challenge, you must use this output redirection to write the word `PWN` (all uppercase) to the filename `COLLEGE` (all uppercase).

## Solution:

After the terminal comes up, the user needs to write the word `PWN` into the file `COLLEGE`, this can be done using the command `echo PWN > COLLEGE`.

#### Commands run:

```sh
$ echo PWN > COLLEGE
```

## Flag: 

```
pwn.college{gZIIUmyuepsAx2NHj9LhB2S34DQ.QX0YTN0wyM1EzNzEzW}
```

### Notes:

- Redirecting stdout to files can be done using the `>`.
- `echo` command can be used to write into a file.


# Challenge 2 Redirecting More Output

Aside from redirecting the output of `echo`, you can, of course, redirect the output of any command.
In this level, `/challenge/run` will once more give you a flag, but _only_ if you redirect its output to the file `myflag`.
Your flag will, of course, end up in the `myflag` file!

You'll notice that `/challenge/run` will still happily print to your terminal, despite you redirecting stdout.
That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out!

## Solution:

After the terminal comes up, the user needs to redirect the stdout (ie: the flag) of the function `/challenge/run` into the file `myflag`, this can be done using the command `/challenge/run > myflag`.

Next the user needs to read the flag from the `myflag` file using the command `cat myflag`.

#### Commands run:

```sh
$ /challenge/run > myflag
$ cat myflag
```

## Flag: 

```
pwn.college{8cKl3vGAWx-80gonJCNkN7dhvc8.QX1YTN0wyM1EzNzEzW}
```

### Notes:

- The stdout of functions can also be redirected into other files using the `>` command.


# Challenge 3 Appending output

A common use-case of output redirection is to save off some command results for later analysis.
Often times, you want to do this in _aggregate_: run a bunch of commands, save their output, and `grep` through it later.
In this case, you might want all that output to keep appending to the same file, but `>` will create a new output file every time, deleting the old contents.

You can redirect input in _append_ mode using `>>` instead of `>`, as so:

```sh
hacker@dojo:~$ echo pwn > outfile
hacker@dojo:~$ echo college >> outfile
hacker@dojo:~$ cat outfile
pwn
college
hacker@dojo:$
```

To practice, run `/challenge/run` with an append-mode redirect of the output to the file `/home/hacker/the-flag`.
The practice will write the first half of the flag to the file, and the second half to `stdout` if `stdout` is redirected to the file.
If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in _truncation_ mode (`>`), the second half will _overwrite_ the first and you won't get the flag!

Go for it now!


## Solution:

After the terminal comes up, the user needs to redirect the output of `/challenge/run` to the file `/home/hacker/the-flag` in append mode, this can be done using the command `/challenge/run >> /home/hacker/the-flag`. This will write the first half of the flag to the file.

The user can run the same command again to write the second half of the flag without overwriting the first half, ie: `/challenge/run >> /home/hacker/the-flag`.

Now the flag can be read using the command `cat /home/hacker/the-flag`.

#### Commands run:

```sh
$ /challenge/run >> /home/hacker/the-flag
$ /challenge/run >> /home/hacker/the-flag
$ cat /home/hacker/the-flag
```

## Flag: 

```
pwn.college{I2Vm2YqPIz2qPwvAoLnsQk3Vfvn.QX3ATO0wyM1EzNzEzW}
```

### Notes:

- We can redirect input in _append_ mode using `>>` instead of `>`
- Redirecting in _truncate_ mode (`>`) overwrites the contents of a file/creates a new file.


# Challenge 4 Redirecting Errors

Just like standard output, you can also redirect the error channel of commands.
Here, we'll learn about *File Descriptor numbers*.
A File Descriptor (FD) is a number that *describes* a communication channel in Linux.
You've already been using them, even though you didn't realize it.
We're already familiar with three:

- FD 0: Standard Input
- FD 1: Standard Output
- FD 2: Standard Error

When you redirect process communication, you do it by FD number, though some FD numbers are implicit.
For example, a `>` without a number implies `1>`, which redirects FD 1 (Standard Output).
Thus, the following two commands are equivalent:

```sh
hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
```

Redirecting errors is pretty easy from this point.
If you have a command that might produce data via standard error (such as `/challenge/run`), you can do:

```sh
hacker@dojo:~$ /challenge/run 2> errors.log
```

That will redirect standard error (FD 2) to the `errors.log` file.
Furthermore, you can redirect multiple file descriptors at the same time!
For example:

```sh
hacker@dojo:~$ some_command > output.log 2> errors.log
```

That command will redirect output to `output.log` and errors to `errors.log`.

Let's put this into practice!
In this challenge, you will need to redirect the output of `/challenge/run`, like before, to `myflag`, and the "errors" (in our case, the instructions) to `instructions`.
You'll notice that nothing will be printed to the terminal, because you have redirected everything!
You can find the instructions/feedback in `instructions` and the flag in `myflag` when you successfully pull this off!

## Solution:

After the terminal comes up, the user needs to redirect the output of `/challenge/run` to `myflag` and redirect the errors to `instructions`, this can be done using the command `/challenge/run > myflag 2> instructions`.

Now the flag can be read using the command `cat myflag`.

#### Commands run:

```sh
$ /challenge/run > myflag 2> instructions
$ cat myflag
```

## Flag: 

```
pwn.college{Ymojle8I0p1Jy9CjDbZL8FYJdYs.QX3YTN0wyM1EzNzEzW}
```

### Notes:

- FD0: Standard Input, FD1: Standard Output, FD2: Standard Error
- Errors can be redirected using `2>`.
- We can redirect multiple file descriptors at the same time ex: `some_command > output.log 2> errors.log`.


# Challenge 5 Redirecting Input

Just like you can redirect _output_ from programs, you can redirect input _to_ programs!
This is done using `<`, as so:

```sh
hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
```

You can do interesting things with a lot of different programs using input redirection!
In this level, we will practice using `/challenge/run`, which will require you to redirect the `PWN` file to it and have the `PWN` file contain the value `COLLEGE`!
To write that value to the `PWN` file, recall the prior challenge on output redirection from `echo`!

## Solution:

After the terminal comes up, the user needs to first write the valoe `COLLEGE` into the file `PWN`, this can be done using the command `echo COLLEGE > PWN`.

Next the user needs to provide this file as standard input to the function `/challenge/run`, this can be done using the command `/challenge/run < PWN`.

#### Commands run:

```sh
$ echo COLLEGE > PWN
$ /challenge/run < PWN
```

## Flag: 

```
pwn.college{Av1gT1aYrVfGaqAKkv0Ungcv9ct.QXwcTN0wyM1EzNzEzW}
```

### Notes:

- Standard Input can be provided to programs using `<` in the shell.


# Challenge 6 Grepping Stored Results

You know how to run commands, how to redirect their output (e.g., `>`), and how to search through the resulting file (e.g., `grep`).
Let's put this together!

In preparation for more complex levels, we want you to:

1. Redirect the output of `/challenge/run` to `/tmp/data.txt`.
2. This will result in a hundred thousand lines of text, with one of them being the flag, in `/tmp/data.txt`.
3. `grep` that for the flag!

## Solution:

After the terminal comes up, first the user needs to redirect the output of `/challenge/run` to the file `/tmp/data.txt`, this can be done using the command `/challenge/run > /tmp/data.txt`.

Next the user needs to `grep` for the flag in `/tmp/data.txt`, this can be done using the command `grep flag /tmp/data.txt`.

#### Commands run:

```sh
$ /challenge/run > /tmp/data.txt
$ grep flag /tmp/data.txt
```

## Flag: 

```
pwn.college{ErEZO2R5uiq17NxFGGoFgFHjlyN.QX4EDO0wyM1EzNzEzW}
```

### Notes:

- We can store outputs/errors of programs to files and then grep them later.


# Challenge 7 Grepping Live Output

It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level.
You can do this by using the `|` (pipe) operator.
Standard output from the command to the left of the pipe will be connected to (_piped into_) the standard input of the command to the right of the pipe.
For example:

```sh
hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
```

Now try it for yourself! `/challenge/run` will output a hundred thousand lines of text, including the flag.
`grep` for the flag!

## Solution:

After the terminal comes up, the user needs to `grep` the output of the program `/challenge/run` for the flag, this can be done using the command `/challenge/run | grep pwn.college`.

#### Commands run:

```sh
$ /challenge/run | grep pwn.college
```

## Flag: 

```
pwn.college{8x64prMxRozWriBvPoN2ZKKxbHZ.QX5EDO0wyM1EzNzEzW}
```

### Notes:

- Standard output from the command to the left of the pipe will be connected to (_piped into_) the standard input of the command to the right of the pipe.


# Challenge 8 Grepping Errors

You know how to redirect errors to a file, and you know how to pipe output to another program, such as `grep`.
But what if you wanted to `grep` through errors directly?

The `>` operator redirects a given file descriptor to a file, and you've used `2>` to redirect fd 2, which is standard error.
The `|` operator redirects _only standard output_ to another program, and there is no `2|` form of the operator!
It can _only_ redirect standard output (file descriptor 1).

Luckily, where there's a shell, there's a way!

The shell has a `>&` operator, which redirects a file descriptor _to another file descriptor_.
This means that we can have a two-step process to `grep` through errors: first, we redirect standard error to standard output (`2>& 1`) and then pipe the now-combined stderr and stdout as normal (`|`)!

Try it now!
Like the last level, this level will overwhelm you with output, but this time on standard error.
`grep` through it to find the flag!

## Solution:

After the terminal comes up, the user needs to first output the standard errors of `/challenge/run` program, convert it into a standard output then pipe it as standard input into the `grep` function to get the flag, this can be done using the command `/challenge/run 2>& 1 | grep pwn.college`.

#### Commands run:

```sh
$ /challenge/run 2>& 1 | grep pwn.college
```

## Flag: 

```
pwn.college{cKK0ZH09Nm1Siriq3dUXu7fu2wJ.QX1ATO0wyM1EzNzEzW}
```

### Notes:

- The `|` operator redirects _only standard output_ to another program, and there is no `2|` form of the operator.
- Shell has a `>&` operator, which redirects a file descriptor _to another file descriptor_.
- we redirect standard error to standard output using `2>& 1`.


# Challenge 9 Filtering with grep -v

The `grep` command has a very useful option: `-v` (invert match).
While normal `grep` shows lines that MATCH a pattern, `grep -v` shows lines that do NOT match a pattern:

```sh
hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
```

Sometimes, the only way to filter to just the data you want is to filter _out_ the data you _don't_ want.
In this challenge, `/challenge/run` will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word `DECOY` somewhere in the flag) mixed in with the real flag.
You'll need to filter _out_ the decoys while keeping the real flag!

Use `grep -v` to filter out all the lines containing "DECOY" and reveal the real flag!

## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` program which outputs (FD1) decoy flags containing the word `DECOY`, then `grep -v` to find the flag. This can be done using the command `/challenge/run | grep -v DECOY`.

#### Commands run:

```sh
$ /challenge/run | grep -v DECOY
```

## Flag: 

```
pwn.college{UXxtyO9zKwhNG7FfjQ6PC0Sy5cf.0FOxEzNxwyM1EzNzEzW}
```

### Notes:

- `grep -v` shows lines that do NOT match a pattern.


# Challenge 10 Duplicating piped data with tee

When you pipe data from one command to another, you of course no longer see it on your screen.
This is not always desired: for example, you might want to see the data as it flows through between your commands to debug unintended outcomes (e.g., "why did that second command not work???").

Luckily, there is a solution!
The `tee` command, named after a "T-splitter" from _plumbing_ pipes, duplicates data flowing through your pipes to any number of files provided on the command line.
For example:

```sh
hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
```

As you can see, by providing two files to `tee`, we ended up with three copies of the piped-in data: one to stdout, one to the `pwn` file, and one to the `college` file.
You can imagine how you might use this to debug things going haywire:

```sh
hacker@dojo:~$ command_1 | command_2
Command 2 failed!
hacker@dojo:~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:~$ command_1 --succeed | command_2
Commands succeeded!
```

Now, you try it!
This process' `/challenge/pwn` must be piped into `/challenge/college`, but you'll need to intercept the data to see what `pwn` needs from you!

## Solution:

After the terminal comes up, the user needs to pipe the output (FD1) of `/challenge/pwn` to `/challenge/college` but intercept this data to find what `pwn` requires to give the correct flag, this can be done using the command `/challenge/pwn | tee intercept | /challenge/college`.

Next the user can read the contents of `intercept` using the command `cat intercept`. this shows us that
```
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "4V-ZNxE2"
```

Now the user can pass the `/challenge/pwn` command using the correct argument `--secret 4V-ZNxE2`, then pipe the output to `/challenge/college`. This can be done using the command `/challenge/pwn --secret 4V-ZNxE2 | /challenge/college`.

#### Commands run:

```sh
$ /challenge/pwn | tee intercept | /challenge/college
$ cat intercept
$ /challenge/pwn --secret 4V-ZNxE2 | /challenge/college
```

## Flag: 

```
pwn.college{4V-ZNxE26HfmgttjLlzlBHnHWPf.QXxITO0wyM1EzNzEzW}
```

### Notes:

- The `tee` command, duplicates data flowing through your pipes to any number of files provided on the command line.
- After the `tee` command has duplicated the command, we need to add another `|` to pipe output to another command,
ex: `/challenge/pwn | tee intercept | /challenge/college`.


# Challenge 11 Process Substitution for input

Sometimes you need to compare the output of two commands rather than two files.
You might think to save each output to a file first:

```sh
hacker@dojo:~$ command1 > file1
hacker@dojo:~$ command2 > file2
hacker@dojo:~$ diff file1 file2
```

But there's a more elegant way! Linux follows the philosophy that ["everything is a file"](https://en.wikipedia.org/wiki/Everything_is_a_file).
That is, the system strives to provide file-like access to most resources, including the input and output of running programs!
The shell follows this philosophy, allowing you to, for example, use any utility that takes file arguments on the command line and hook it up to the output of programs, as you learned in the previous few levels.

Interestingly, we can go further, and hook input and output of programs to _arguments_ of commands.
This is done using [Process Substitution](https://www.gnu.org/software/bash/manual/html_node/Process-Substitution.html).
For reading from a command (input process substitution), use `<(command)`.
When you write `<(command)`, bash will run the command and hook up its output to a temporary file that it will create.
This isn't a _real_ file, of course, it's what's called a _named pipe_, in that it has a file name:

```sh
hacker@dojo:~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:~$
```

Where did `/dev/fd/63` come from?
`bash` replaced `<(echo hi)` with the path of the named pipe file that's hooked up to the command's output!
While the command is running, reading from this file will read data from the standard output of the command.
Typically, this is done using commands that take input files as arguments:

```sh
hacker@dojo:~$ cat <(echo hi)
hi
hacker@dojo:~$
```

Of course, you can specify this multiple times:

```sh
hacker@dojo:~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:~$
```

Now for your challenge!
Recall what you learned in the `diff` challenge from [Comprehending Commands](/linux-luminarium/commands).
In that challenge, you diffed two files.

Now, you'll diff two sets of command outputs: `/challenge/print_decoys`, which will print a bunch of decoy flags, and `/challenge/print_decoys_and_flag` which will print those same decoys plus the real flag.

Use process substitution with `diff` to compare the outputs of these two programs and find your flag!

## Solution:

After the terminal comes up, the user needs to `diff` 2 sets of command inputs; `/challenge/print_decoys` and `/challenge/print_decoys_and_flag`, this can be done using the command `diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)`.

#### Commands run:

```sh
$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
```

## Flag: 

```
pwn.college{Qg98Fi4tkaX64HdwishPVYomtJt.0lNwMDOxwyM1EzNzEzW}
```

### Notes:

- Linux follows the philosophy that ["everything is a file"](https://en.wikipedia.org/wiki/Everything_is_a_file).
- We can hook input and output of programs to _arguments_ of commands. This is done using [Process Substitution](https://www.gnu.org/software/bash/manual/html_node/Process-Substitution.html).
- For reading from a command (input process substitution), use `<(command)`.


# Challenge 12 Writing to multiple programs

Now you've learned that process substitution can make command output appear as files for reading with `<(command)`.
But you can also use process substitution for _writing_ to commands!

You can duplicate data to two files with `tee`:

```console
hacker@dojo:~$ echo HACK | tee THE > PLANET
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$ cat PLANET
HACK
hacker@dojo:~$
```

And you've used `tee` to duplicate data to a file and a command:

```console
hacker@dojo:~$ echo HACK | tee THE | cat
HACK
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$
```

But what about duplicating to two commands?
As `tee` says in its manpage, it's designed to write to files and to standard output:

```text
TEE(1)                           User Commands                          TEE(1)

NAME
       tee - read from standard input and write to standard output and files
```

But wait! You just learned that bash can make commands look like files using process substitution!
For writing to a command (output process substitution), use `>(command)`.
If you write an argument of `>(rev)`, bash will run the `rev` command (this command reads data from standard input, reverses its order, and writes it to standard output!), but hook up its input to a temporary named pipe file.
When commands write to this file, the data goes to the standard input of the command:

```console
hacker@dojo:~$ echo HACK | rev
KCAH
hacker@dojo:~$ echo HACK | tee >(rev)
HACK
KCAH
```

Above, the following sequence of events took place:

1. `bash` started up the `rev` command, hooking a named pipe (presumably `/dev/fd/63`) to `rev`'s standard input
2. `bash` started up the `tee` command, hooking a pipe to its standard input, and replacing the first argument to `tee` with `/dev/fd/63`. `tee` never even saw the argument `>(rev)`; the shell _substituted_ it before launching `tee`
3. `bash` used the `echo` builtin to print `HACK` into `tee`'s standard input
4. `tee` read `HACK`, wrote it to standard output, and then wrote it to `/dev/fd/63` (which is connected to `rev`'s stdin)
5. `rev` read `HACK` from its standard input, reversed it, and wrote `KCAH` to standard output

Now it's your turn!
In this challenge, we have `/challenge/hack`, `/challenge/the`, and `/challenge/planet`.
Run the `/challenge/hack` command, and duplicate its output as input to both the `/challenge/the` and the `/challenge/planet` commands!
Scroll back through the previous challenges "Duplicating piped data with tee" and "Process substitution for input" if you need a refresher on this method.

----
**Trivia!**

The observant learner will realize that the following are equivalent:

```console
hacker@dojo:~$ echo hi | rev
ih
hacker@dojo:~$ echo hi > >(rev)
ih
hacker@dojo:~$
```

More than one way to pipe data!
Of course, the second route is way harder to read and also harder to expand.
For example:

```console
hacker@dojo:~$ echo hi | rev | rev
hi
hacker@dojo:~$ echo hi > >(rev | rev)
hi
hacker@dojo:~$
```

That's just silly!
The lesson here is that, while Process Substitution is a powerful tool in your toolbox, it's a very _specialized_ tool; don't use it for everything!

## Solution:

Describe your thought process and solve, write as much as possible with steps:

- 
- 
- 

Use this blob for pasting commands you've run
```sh
$ cat flag
pwn.college{}
```

## Flag: 

```
pwn.college{ }
```


### References:

- [link 1](https://pwn.college)
- 
### Notes:

Include things you learnt, alternate methods or mistakes you made while solving


