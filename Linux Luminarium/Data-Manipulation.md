
# Challenge 1 Translating Characters

One of the purposes of piping data is to _modify_ it.
Many Linux commands will help you modify data in really cool ways.
One of these is `tr`, which `tr`anslates characters it receives over standard input and prints them to standard output.

In its most basic usage, `tr` translates the character provided in its first argument to the character provided in its second argument:

```sh
hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
```

It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

```sh
hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
```

Now, you try it!
In this level, `/challenge/run` will print the flag but will swap the casing of all characters (e.g., `A` will become `a` and vice-versa).
Can you undo it with `tr` and get the flag?


## Solution:

After the terminal comes up, the user needs to swap the cases of all characters of the output of `/challenge/run`, this can be done using the `tr` command. The argument to `tr` would be all lower and upper case characters and the second argument will be all upper and lower case characters. The command is 

`/challenge/run | tr qQwWeErRtTyYuUiIoOpPaAsSdDfFgGhHjJkKlLzZxXcCvVbBnNmM QqWwEeRrTtYyUuIiOoPpAaSsDdFfGgHhJjKkLlZzXxCcVvBbNnMm`.

#### Commands run:

```sh
$ /challenge/run | tr qQwWeErRtTyYuUiIoOpPaAsSdDfFgGhHjJkKlLzZxXcCvVbBnNmM QqWwEeRrTtYyUuIiOoPpAaSsDdFfGgHhJjKkLlZzXxCcVvBbNnMm
```

## Flag: 

```
pwn.college{sYb38Fw6pEbrWrkrUgrkTcW9hps.01MxEzNxwyM1EzNzEzW}
```

### Notes:

- In its most basic usage, `tr` translates the character provided in its first argument to the character provided in its second argument.


# Challenge 2 Deleting Characters

`tr` can also translate characters to nothing (i.e., _delete_ them).
This is done via a `-d` flag and an argument of what characters to delete:

```sh
hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
```

Pretty simple!
Now you give it a try.
I'll intersperse some decoy characters (specifically: `^` and `%`) among the flag characters.
Use `tr -d` to remove them!


## Solution:

After the terminal comes up, the user needs to invoke the `/challenge/run` command and delete all occurances of `^%`, This can be done using the command `/challenge/run | tr -d %^`.

#### Commands run:

```sh
$ /challenge/run | tr -d %^
```

## Flag: 

```
pwn.college{cM6LbKxV6l6-wpgvsNsA_1H2qSg.0FNxEzNxwyM1EzNzEzW}
```

### Notes:

- `tr` can also translate characters to nothing (i.e., _delete_ them). This is done via a `-d` flag and an argument of what characters to delete.


# Challenge 3 Deleting newlines

A common class of characters to remove is a line separator.
This happens when you have a stream of data that you want to turn into a single line for further processing.
You can specify newlines almost like any other character, by _escaping_ them:

```sh
hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
```

Here, the backslash (`\`) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally.
The newline, of course, is hard to input because when you typically hit `Enter`, you'll run the command itself.
`\n` is a standin for this newline, and it _must_ be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to `tr` instead.

Now, let's combine this with deletion.
In this challenge, we'll inject a bunch of newlines into the flag.
Delete them with `tr`'s `-d` flag and the _escaped_ newline specification!

----

**Fun fact!**
Want to _actually_ replace a backslash (`\`) character?
Because `\` is the escape character, you gotta escape it!
`\\` will be treated as a backslash by `tr`.
This isn't relevant to this challenge, but is a fun fact nonetheless!

## Solution:

After the terminal comes up, the user needs to invoke thee `/challenge/run` and delete the newlines from the output, this can be done using the command `/challenge/run | tr -d "\n"`.

#### Commands run:

```sh
$ /challenge/run | tr -d "\n"
```

## Flag: 

```
pwn.college{wvYQcZlnJCEE2Kw5PxlnOi-QQQU.0VNxEzNxwyM1EzNzEzW}
```

### Notes:

- In shell the newline character is represented with the `\n` escape sequence, and it must be in quotes.


# Challenge 4 Extracting the first lines with head

In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs.
For this, you'll reach for `head`!
The `head` command is used to display the first few lines of its input:

```sh
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```

By default, it shows the first 10 lines, but you can control this with the `-n` option:

```sh
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```

This challenge's `/challenge/pwn` outputs a bunch of data, and you'll need to pipe it through `head` to grab just the first 7 lines and then pipe them onwards to `/challenge/college`, which will give you the flag if you do this right!
Your solution will be a long composite command with _two_ pipes connecting three commands.
Good luck!

## Solution:

After the terminal comes up, the user needs to invoke `/challenge/pwn` and pipe the first `7` lines to `/challenge/college`, this can be done using the command `/challenge/pwn | head -n 7 | /challenge/college`.

#### Commands run:

```sh
$ /challenge/pwn | head -n 7 | /challenge/college
```

## Flag: 

```
pwn.college{0wX7P949V9-TcmrQ4lekKKwZU7E.0lNxEzNxwyM1EzNzEzW}
```

### Notes:

- The `head` command is used to display the first few lines of its input.


# Challenge 5 Extracting Specific sections of text

Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column.
For this, there's the `cut` command.

For example, imagine that you have the following data file:

```sh
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```

You could use `cut` to extract specific columns:

```sh
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```

The `-d` argument specifies the column _delimiter_ (how columns are separated).
In this case, it's a space character.
Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments!
The `-f` argument specifies the _field_ number (which column to extract).

In this challenge, the `/challenge/run` program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns.
Use `cut` to extract the flag characters, then pipe them to `tr -d "\n"` (like the previous level!) to join them together into a single line.
Your solution will look something like `/challenge/run | cut ??? | tr ???`, with the `???` filled out.


## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` and only requires the 2nd collumn of each line, in a single line. This can be done by piping the output (FD1) to `cut` function then piping the output (FD1) to `tr` function using the command `/challenge/run | cut -d " " -f 2 | tr -d "\n"`.

#### Commands run:

```sh
$ /challenge/run | cut -d " " -f 2 | tr -d "\n"
```

## Flag: 

```
pwn.college{o3rMTyERKqR_6uODr6bWR9LVQbw.01NxEzNxwyM1EzNzEzW}
```

### Notes:

- We can grab specific columns of data using the `cut` command.
- The `-d` argument specifies the column _delimiter_ (how columns are separated), The `-f` argument specifies the _field_ number (which column to extract).


# Challenge 6 Sorting data

Files (or output lines of commands) aren't always in the order you need them!
The `sort` command helps you organize data.
It reads lines from input (or files) and outputs them in sorted order:

```sh
hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
```

By default, `sort` orders lines alphabetically.
Arguments can change this:

- `-r`: reverse order (Z to A)
- `-n`: numeric sort (for numbers)
- `-u`: unique lines only (remove duplicates)
- `-R`: random order!

In this challenge, there's a file at `/challenge/flags.txt` containing 100 fake flags, with the real flag mixed among them.
When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags).
Go get it!


## Solution:

After the terminal comes up, the user needs to sort `/challenge/flags.txt` alphabetically and will obtain the real flag at the last, this can be done using the command `sort /challenge/flags.txt`.

#### Commands run:

```sh
$ sort /challenge/flags.txt
```

## Flag: 

```
pwn.college{AZxT-b_eaUFCbiK1jMTE8h4vsf4.0FM0MDOxwyM1EzNzEzW}
```

### Notes:

- The `sort` command helps you organize data by default, `sort` orders lines alphabetically.
- `-r`: reverse order (Z to A), `-n`: numeric sort (for numbers), `-u`: unique lines only (remove duplicates), `-R`: random order!
