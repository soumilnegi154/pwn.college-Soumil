
# Challenge 1 Printing Variables

Let's start with printing variables out.
The `/challenge/run` program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"!
Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with `echo`.
This command just prints stuff.
For example:

```sh
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
```

You can also print out variables with `echo`, by prepending the variable name with a `$`.
For example, there is a variable, `PWD`, that always holds the current working directory of the current shell.
You print it out as so:

```sh
hacker@dojo:~$ echo $PWD
/home/hacker
```

Now it's your turn.
Have your shell print out the `FLAG` variable and solve this challenge!

## Solution:

After the terminal comes up, first the user needs to invoke the program `/challenge/run` which stores the flag in a variable called `FLAG`.

Then the user needs to print the variable `FLAG`, this can be done using the command `echo $FLAG`.

#### Commands run:

```sh
$ /challenge/run
$ echo $FLAG
```

## Flag: 

```
pwn.college{MSfSGyvyDlLkFwioChdJHGqPJe_.QX3UTN0wyM1EzNzEzW}
```

### Notes:

- Accessing variables in shell start with `$`. ex: `$FLAG`.
- Variables can be printed in shell using `echo`.
- Variable `PWD` always holds the current working directory.


# Challenge 2 Setting Variables

Naturally, as well as reading values stored in variables, you can write values to variables.
This is done, as with many other languages, using `=`.
To set variable `VAR` to value `1337`, you would use:

```sh
hacker@dojo:~$ VAR=1337
```

Note that there are no spaces around the `=`!
If you put spaces (e.g., `VAR = 1337`), the shell won't recognize a variable assignment and will, instead, try to run the `VAR` command (which does not exist).

Also note that this uses `VAR` and *not* `$VAR`: the `$` is only prepended to *access* variables.
In shell terms, this prepending of `$` triggers what is called *variable expansion*, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:

```sh
hacker@dojo:~$ echo $VAR
1337
```

To solve this level, you must set the `PWN` variable to the value `COLLEGE`.
Be careful: both the names and values of variables are case-sensitive!
`PWN` is not the same as `pwn` and `COLLEGE` is not the same as `College`.

## Solution:

After the terminal comes up, the user needs to assign the value `COLLEGE` to the variable `PWD`, this can be done using the command `PWD=COLLEGE`.

#### Commands run:

```sh
$ PWD=COLLEGE
```

## Flag: 

```
pwn.college{k9ooFvle2M0vf8NTjaeHAb5V2s7.QX5UTN0wyM1EzNzEzW}
```

### Notes:

- `=` can be used to assign value to a variable.
- There should be no spaces around `=`, if there are spaces then the shell will try to run the variable as a program.
-  the `$` is only prepended to *access* variables. In shell terms, this prepending of `$` triggers what is called *variable expansion*, and is the source of many potential vulnerabilities.


# Challenge 3 Multi-Word Variables

In this level, you will learn about quoting.
Spaces have special significance in the shell, and there are places where you can't use them spuriously.
Recall our variable setting:

```sh
hacker@dojo:~$ VAR=1337
```

That sets the `VAR` variable to `1337`, but what if you wanted to set it to `1337 SAUCE`?
You might try the following:

```sh
hacker@dojo:~$ VAR=1337 SAUCE
```

This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the `=`.
When the shell sees a space, it ends the variable assignment and interprets the next word (`SAUCE` in this case) as a command.
To set `VAR` to `1337 SAUCE`, you need to *quote* it:

```sh
hacker@dojo:~$ VAR="1337 SAUCE"
```

Here, the shell reads `1337 SAUCE` as a single token, and happily sets that value to `VAR`.
In this level, you'll need to set the variable `PWN` to `COLLEGE YEAH`.
Good luck!

## Solution:

After the terminal comes up, the user needs to assign the value `COLLEGE YEAH` to the variable `PWN`, this can be done using the command `PWN="COLLEGE YEAH"`.

#### Commands run:

```sh
$ PWN="COLLEGE YEAH"
```

## Flag: 

```
pwn.college{ksc2VMcyYqp4qotGvzvHNM0zmBW.QXwYTN0wyM1EzNzEzW}
```

### Notes:

- When assigning multi word value to a variable, we need to include it in quotes, otherwise shell will run it like an command.


# Challenge 4 Exporting Variables

By default, variables that you set in a shell session are local to that shell process.
That is, other commands you run won't inherit them.
You can experiment with this by simply invoking another shell process in your own shell, like so:

```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 
```

In the output above, the `$` prompt is the prompt of `sh`, a minimal shell implementation that is invoked as a *child* of the main shell process.
And it does not receive the `VAR` variable!

This makes sense, of course.
Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should.
How do you mark that it should?
You *export* your variables.
When you export your variables, they are passed into the *environment variables* of child processes.
You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here.
Here is an example:

```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

Here, the child shell received the value of VAR and was able to print it out!
You can also combine those first two lines.

```sh
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

In this challenge, you must invoke `/challenge/run` with the `PWN` variable exported and set to the value `COLLEGE`, and the `COLLEGE` variable set to the value `PWN` but *not* exported (e.g., not inherited by `/challenge/run`).
Good luck!


## Solution: 

After the terminal comes up, the user needs to set the value of variable `COLLEGE` to `PWN`, and variable `PWN` to `COLLEGE`. This can be done using the commands `COLLEGE=PWN` and `PWN=COLLEGE`.

Then the user needs to export only the `PWN` variable, this can be done using the command `export PWN`.

Then the user needs to invoke the `/challenge/run` program to get the flag, this can be done using the command `/challenge/run`.

#### Commands run:


```sh
$ COLLEGE=PWN
$ PWN=COLLEGE
$ export PWN
$ /challenge/run
```

## Flag: 

```
pwn.college{gM--3SVS_-1qrcQMa0qwScE__yy.QXyYTN0wyM1EzNzEzW}
```

### Notes:

- By default Variables that you set in a shell session are local to that shell process.
- The `$` prompt is the prompt of `sh`, a minimal shell implementation that is invoked as a *child* of the main shell process.
- When you export your variables, they are passed into the *environment variables* of child processes.


# Challenge 5 Printing Exported Variables

There are multiple ways to access variables in bash.
`echo` was just one of them, and we'll now learn at least one more in this challenge.

Try the `env` command: it'll print out every _exported_ variable set in your shell, and you can look through that output to find the `FLAG` variable!


## Solution:

After the terminal comes up, the user needs to invoke the `env` function using the command `env`, this outputs

```
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=5270dee61ec51f3215254f3d1c3d097b596ef0e3ca1340a77b2a35f3ebd323ad
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{U0onAHYl7C0dUuv2dOG-TzdJGYI.QX4UTN0wyM1EzNzEzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
```

Here the user can find the value of flag variable.

#### Commands run:

```sh
$ env
```

## Flag: 

```
pwn.college{U0onAHYl7C0dUuv2dOG-TzdJGYI.QX4UTN0wyM1EzNzEzW}
```

### Notes:

-  The `env` command: it'll print out every _exported_ variable set in your shell.


# Challenge 6 Storing Command Output

In the course of working with the shell, you will often want to store the output of some command into a variable.
Luckily, the shell makes this quite easy using something called [_Command Substitution_](https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html)!
Observe:

```sh
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```

Neat!
Now, you practice.
Read the output of the `/challenge/run` command directly into a variable called `PWN`, and it will contain the flag!

----
**Trivia:**
You can also use backticks instead of `$()`: `` FLAG=`cat /flag` `` instead of ``FLAG=$(cat /flag)`` in the example above.
This is an older format, and has some disadvantages (for example, imagine if you wanted to _nest_ command substitutions).
How would you do `$(cat $(find / -name flag))` with backticks?
The official stance of pwn.college is that you should use `$(blah)` instead of `` `blah` ``.

## Solution:

After the terminal comes up, the user needs to set the value of the variable `PWN` as the output of `/challenge/run`, this can be done using the command `PWN=$(/challenge/run)`.

Then the user can print the variable using the command `echo $PWN` and get the flag.

#### Commands run:

```sh
$ PWN=$(/challenge/run)
$ echo $PWN
```

## Flag: 

```
pwn.college{EcS4VM0Qews9-hKq8EXB915wM5W.QX1cDN1wyM1EzNzEzW}
```

### Notes:

- We can store the output of commands to a variable using  [_Command Substitution_](https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html).
- example: `FLAG=$(cat /flag)`.


# Challenge 7 Reading Input

We'll start with reading input from the user (you).
That's done using the aptly named `read` builtin, which *reads* input into a variable!

Here is an example using the `-p` argument, which lets you specify a prompt (otherwise, it would be hard for you, reading this now, to separate input from output in the example below):

```sh
hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
```

Keep in mind, `read` reads data from your standard input!
The first `Hello!`, above, was _inputted_ rather than _outputted_.
Let's try to be more explicit with that.
Here, we annotated the beginning of each line with whether the line represents `INPUT` from the user or `OUTPUT` to the user:

```sh
 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
```

In this challenge, your job is to use `read` to set the `PWN` variable to the value `COLLEGE`.
Good luck!


## Solution:

After the terminal comes up, the user needs to read the input `COLLEGE` and set it to the variable `PWN`. This can be done using the command `read -p "Input: " PWN`.

Then the user needs to enter the `Input: ` as `COLLEGE` and will get the flag.

#### Commands run:

```sh
$ read -p "Input: " PWN
Input: COLLEGE
```

## Flag: 

```
pwn.college{EZnCRxiwT5264lENszELPkpHfwo.QX4cTN0wyM1EzNzEzW}
```

### Notes:

- `read` builtin *reads* input into a variable.
- `-p` argument lets you specify a prompt. Ex: `read -p "Input: " PWN`.


# Challenge 8 Reading Files

Often, when shell users want to read a file into an environment variable, they do something like:

```sh
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
```

This works, but it represents what grouchy hackers call a ["Useless Use of Cat"](https://porkmail.org/era/unix/award#cat).
That is, running a whole other program just to read the file is a waste.
It turns out that you can just use the powers of the shell!

Previously, you `read` user input into a variable.
You've also previously redirected files into command input!
Put them together, and you can read files with the shell.

```sh
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
```

What happened there?
The example redirects `some_file` into the *standard input* of `read`, and so when `read` reads into `VAR`, it reads from the file!
Now, use that to read `/challenge/read_me` into the `PWN` environment variable, and we'll give you the flag!
The `/challenge/read_me` will keep changing, so you'll need to read it right into the `PWN` variable with one command!

## Solution:

After the terminal comes up, the user needs to read into the variable `PWN` and to its input (FD0) redirect the `/challenge/read_me` file. This can be done using the command `read PWN < /challenge/read_me`.

#### Commands run:

```sh
$  read PWN < /challenge/read_me
```

## Flag: 

```
pwn.college{cRdHnqrM867FqzLskI5pgPMDUZ_.QXwIDO0wyM1EzNzEzW}
```

### Notes:

- We can also redirect files to stdinp of read variables.















