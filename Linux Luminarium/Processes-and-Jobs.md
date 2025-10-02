
# Challenge 1 Listing Processes

First, we will learn to list running processes using the `ps` command.
Depending on whom you ask, `ps` either stands for "process snapshot" or "process status", and it lists processes.
By default, `ps` just lists the processes running in your terminal, which honestly isn't very useful:

```sh
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```

In the above example, we have the shell (`bash`) and the `ps` process itself, and that's all that's running on that specific terminal.
We also see that each process has a numerical identifier (the _Process ID_, or PID), which is a number that uniquely identifies every running process in a Linux environment.
We also see the terminal on which the commands are running (in this case, the designation `pts/0`), and the total amount of _cpu time_ that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!).

In the majority of cases, this is all that you'll see with a default `ps`.
To make it useful, we need to pass a few arguments.

As `ps` is a very old utility, its usage is a bit of a mess.
There are two ways to specify arguments.

**"Standard" Syntax:** in this syntax, you can use `-e` to list "every" process and `-f` for a "full format" output, including arguments.
These can be combined into a single argument `-ef`.

**"BSD" Syntax:** in this syntax, you can use `a` to list processes for all users, `x` to list processes that aren't running in a terminal, and `u` for a "user-readable" output.
These can be combined into a single argument `aux`.

These two methods, `ps -ef` and `ps aux`, result in slightly different, but cross-recognizable output.

Let's try it in the dojo:

```sh
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```

You can see here that there are processes running for the initialization of the challenge environment (`docker-init`), a timeout before the challenge is automatically terminated to preserve computing resources (`sleep 6h` to timeout after 6 hours), the VSCode environment (several `code-server` helper processes), the shell (`bash`), and my `ps -ef` command.
It's basically the same thing with `ps aux`:

```
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```

There are many commonalities between `ps -ef` and `ps aux`: both display the user (`USER` column), the PID, the TTY, the start time of the process (`STIME`/`START`), the total utilized CPU time (`TIME`), and the command (`CMD`/`COMMAND`).
`ps -ef` additionally outputs the _Parent Process ID_ (`PPID`), which is the PID of the process that launched the one in question, while `ps aux` outputs the percentage of total system CPU and Memory that the process is utilizing.
Plus, there's a bunch of other stuff we won't get into right now.

Anyways!
Let's practice.
In this level, I have once again renamed `/challenge/run` to a random filename, and this time made it so that you cannot `ls` the `/challenge` directory!
But I also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag!
Good luck!

**NOTE:** Both `ps -ef` and `ps aux` truncate the command listing to the width of your terminal (which is why the examples above line up so nicely on the right side of the screen.
If you can't read the whole path to the process, you might need to enlarge your terminal (or redirect the output somewhere to avoid this truncating behavior)!
Alternatively, you can pass the `w` option _twice_ (e.g., `ps -efww` or `ps auxww`) to disable the truncation.


## Solution:

After the terminal comes up, the user needs to see the running processes, this can be done using the command `ps -ef` which shows
```
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 14:52 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-i
root           7       1  0 14:52 ?        00:00:00 /run/dojo/bin/sleep 6h
root         132       1  0 14:52 ?        00:00:00 /challenge/5293-run-31269
root         135     132  0 14:52 ?        00:00:00 sleep 6h
hacker       137       0  0 14:53 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/
hacker       143     137  0 14:53 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       153     143  0 15:13 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/
hacker       154     153  0 15:13 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       164     154  0 15:13 pts/0    00:00:00 ps -ef
```

Here clearly the `/challenge/run` is renamed to `/challenge/5293-run-31269`, thus the user can get the flag by invoking `/challenge/5293-run-31269`.

#### Commands run:

```sh
$ ps -ef
$ /challenge/5293-run-31269
```

## Flag: 

```
pwn.college{8Nx9qX5edR3oLjpDxhnHT76Yypb.QX4MDO0wyM1EzNzEzW}
```

### Notes:

- By default, `ps` just lists the processes running in your terminal.
- **"Standard" Syntax:** in this syntax, you can use `-e` to list "every" process and `-f` for a "full format" output, including arguments. These can be combined into a single argument `-ef`.
- **"BSD" Syntax:** in this syntax, you can use `a` to list processes for all users, `x` to list processes that aren't running in a terminal, and `u` for a "user-readable" output. These can be combined into a single argument `aux`.


# Challenge 2 Killing Processes

You've launched processes, you've viewed processes, now you will learn to _terminate_ processes!
In Linux, this is done using the aggressively-named `kill` command.
With default options (which is all we'll cover in this level), `kill` will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.

Let's say you had a pesky `sleep` process (`sleep` is a program that simply hangs out for the number of seconds specified on the commandline, in this case, 1337 seconds) that you launched in another terminal, like so:

```sh
hacker@dojo:~$ sleep 1337
```

How do we get rid of it?
You use `kill` to terminate it by passing the process identifier (the `PID` from `ps`) as an argument, like so:

```sh
hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
```

Now, it's time to terminate your first process!
In this challenge, `/challenge/run` will refuse to run while `/challenge/dont_run` is running!
You must find the `dont_run` process and `kill` it.
If you fail, `pwn.college` will disavow all knowledge of your mission.
Good luck.


## Solution:

After the terminal comes up, First the user needs to find the pid of the process `/challenge/dont-run`, this can be done using the command `ps -ef | grep dont-run` which shows
```
hacker       136     135  0 15:18 ?        00:00:00 /challenge/dont_run
hacker       156     145  0 15:20 pts/0    00:00:00 grep --color=auto dont_run\
```

Next the user can terminate this process using the command `kill 136`. Now the user can invoke `/challenge/run` and get the flag.

#### Commands run:

```sh
$ ps -ef | grep dont-run
$ kill 136
$ /challenge/run
```

## Flag: 

```
pwn.college{AImx27WbVUPK9uARcuThd28A2fw.QXyQDO0wyM1EzNzEzW}
```

### Notes:

- We can use `kill` to terminate a process by passing the process identifier (the `PID` from `ps`) as an argument.


# Challenge 3 Interrupting Processes

You've learned how to kill other processes with the `kill` command, but sometimes you just want to get rid of the process that's clogging up your terminal!
Luckily, terminals have a hotkey for this: `Ctrl-C` (e.g., holding down the `Ctrl` key and pressing `C`) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

Try it here!
`/challenge/run` will refuse to give you the flag until you interrupt it.
Good luck!

---
For the very interested, check out this [article about terminals and "control codes"](https://catern.com/posts/terminal_quirks.html) (such as `Ctrl-C`).


## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` and then interrupt it using the command `^C` (Pressing `ctrl`+`c`).

#### Commands run:

```sh
$ /challenge/run
$ ^C
```

## Flag: 

```
pwn.college{AcKVpt9Y6zJ3BSHKTaC7b2dVHk9.QXzQDO0wyM1EzNzEzW}
```

### Notes:

- Processes can be interrupted using `Ctrl-C`.


# Challenge 4 Killing Misbehaving Processes

Sometimes, misbehaving processes can interfere with your work.
These processes might need to be killed...

In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at `/tmp/flag_fifo` into which (like in the [Practicing Piping](/linux-luminarium/piping) FIFO challenge) `/challenge/run` wants to write your flag.
You need to `kill` this process.

Your general workflow should be:

1. Check what processes are running.
2. Find `/challenge/decoy` in the list and figure out its process ID.
3. `kill` it.
4. Run `/challenge/run` to get the flag without being overwhelmed by decoys (you don't need to redirect its output; it'll write to the FIFO on its own).

Good luck!

----
**NOTE:**
You might see a few decoy flags show up even after killing the decoy process.
This happens because Linux pipes are _buffered_: conceptually, they have a sort of length through which data flows, and you might kill the decoy process while data is in the pipe.
That data, having already entered the pipe, will proceed to the other end (your `cat`).
If you wait a second, you'll see the decoys stop, and then you can `/challenge/run` and win!


## Solution:

After the terminal comes up, first the user needs to find the pid of `/usr/bin/python/challenge/decoy`, this can be done using the command `ps -ef`, which shows
```
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 15:29 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-i
root           7       1  0 15:29 ?        00:00:00 /run/dojo/bin/sleep 6h
root         137       1  0 15:29 ?        00:00:00 /bin/bash /challenge/.init
root         138       1  0 15:29 ?        00:00:00 /bin/bash /challenge/.init
root         139       1  0 15:29 ?        00:00:00 su -c exec /challenge/decoy > /tmp/flag_fifo hacker
root         140     137  0 15:29 ?        00:00:00 sleep 6h
root         141     138  0 15:29 ?        00:00:00 sleep 6h
hacker       142     139  0 15:29 ?        00:00:00 /usr/bin/python /challenge/decoy
hacker       144       0  0 15:29 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/
hacker       150     144  0 15:29 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       160     150  0 15:30 pts/0    00:00:00 ps -ef
```

Then the user needs to end the process using the command `kill 142`. Now the user can invoke `/challenge/run`, which shows
```
Sending the flag to /tmp/flag_fifo!
```

Now the user can read the flag using `cat /tmp/flag_fifo`.


#### Commands run:

```sh
$ ps -ef
$ kill 142
$ /challenge/run
$ cat /tmp/flag_fifo
```

## Flag: 

```
pwn.college{Epo9GGedX5jmXy9eGWl3EDBzkcc.0FNzMDOxwyM1EzNzEzW}
```

### Notes:

- Linux pipes are _buffered_: conceptually, they have a sort of length through which data flows, and you might kill the decoy process while data is in the pipe. That data, having already entered the pipe, will proceed to the other end (your `cat`).


# Challenge 5 Suspending Processes

You have learned to interrupt processes with `Ctrl-C`, but there are less drastic measures you can use to get your terminal back!
You can _suspend_ processes to the background with `Ctrl-Z`.
In this level, we'll explore how this works and, in the next level, we'll figure out how to _resume_ those suspended processes!

This level's `run` wants to see another copy of itself running _and using the same terminal_.
How?
Use the terminal to launch it, then suspend it, then launch another copy while the first is suspended!


## Solution:

After the terminal comes up, first the user needs to invoke `/challenge/run`, which shows
```
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         228     139  0 15:41 pts/0    00:00:00 bash /challenge/run
root         230     228  0 15:41 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
```

Next the user needs to suspend the process using `^Z`, now the user can invoke a second `/challenge/run` which gives us the flag- 
```
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         228     139  0 15:41 pts/0    00:00:00 bash /challenge/run
root         235     139  0 15:41 pts/0    00:00:00 bash /challenge/run
root         237     235  0 15:41 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{YLHn1-L238MORVdpLuOjCr3cHgp.QX1QDO0wyM1EzNzEzW}
```

#### Commands run:

```sh
$ /challenge/run
$ ^Z
$ /challenge/run
```

## Flag: 

```
pwn.college{YLHn1-L238MORVdpLuOjCr3cHgp.QX1QDO0wyM1EzNzEzW}
```

### Notes:

- We can _suspend_ processes to the background with `Ctrl-Z`.


# Challenge 6 Resuming Processes

Usually, when you suspend processes, you'll want to resume them at some point.
Otherwise, why not just terminate them?
To resume processes, your shell provides the `fg` command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.

Go try it out!
This challenge's `run` needs you to suspend it, then resume it.
Good luck!


## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` which shows
```
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
```

then the user needs to suspend it, using the command `^Z` which shows
```
[1]+  Stopped                 /challenge/run
```

Now the user can resume `/challenge/run` using the command `fg`.
```
/challenge/run
I'm back! Here's your flag:
pwn.college{czMlMkPX_xtZvWcsnVzDlMu5BnM.QX2QDO0wyM1EzNzEzW}
Don't forget to press Enter to quit me!

Goodbye!
```

#### Commands run:

```sh
$ /challenge/run
$ ^Z
$ fg
```

## Flag: 

```
pwn.college{czMlMkPX_xtZvWcsnVzDlMu5BnM.QX2QDO0wyM1EzNzEzW}
```

### Notes:

- We can resume suspended processes using the command `fg`.

# Challenge 7 Backgrounding Processes

You've resumed processes in the _foreground_ with the `fg` command.
You can also resume processes in the _background_ with the `bg` command!
This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

This level's `run` wants to see another copy of itself running, _not suspended_, and using the same terminal.
How?
Use the terminal to launch it, then suspend it, then _background_ it with `bg` and launch another copy while the first is running in the background!

---

**ARCANUM:**
If you're interested in some deeper details, check out how to view the differences between suspended and backgrounded properties!
Allow me to demonstrate.
First, let's suspend a `sleep`:

```sh
hacker@dojo:~$ sleep 1337
^Z
[1]+  Stopped                 sleep 1337
hacker@dojo:~$
```

The `sleep` process is now _suspended_ in the background.
We can see this with `ps` by enabling the `stat` column output with the `-o` option:

```sh
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 T    sleep 1337
hacker       782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
```

See that `T`?
That means that the process is suspended due to our `Ctrl-Z`.
The `S` in `bash`'s `STAT` column means that `bash` is sleeping while waiting for input.
The `R` in `ps`'s column means that it's actively running, and the `+` means that it's in the foreground!

Watch what happens when we resume `sleep` in the background:

```sh
hacker@dojo:~$ bg
[1]+ sleep 1337 &
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 S    sleep 1337
hacker      1224 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```

Boom!
The `sleep` now has an `S`.
It's sleeping while, well, sleeping, but it's not suspended!
It's also in the _background_ and thus doesn't have the `+`.


## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` which shows 
```
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         139 S+   bash /challenge/run
root         141 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
```

Next the user needs to suspend the processes using the command `^Z`.
```
[1]+  Stopped                 /challenge/run
```

Next the user needs to resume the earlier suspended process in background using the command `bg`.
```
[1]+ /challenge/run &
Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
```

Now the user can invoke `/challenge/run` again,
```
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         139 S    bash /challenge/run
root         149 S    sleep 6h
root         150 S+   bash /challenge/run
root         152 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{Mf6VKQ0WzmSoqR-6-Ncm6NAK0sR.QX3QDO0wyM1EzNzEzW}
```

#### Commands run:

```sh
$ /challenge/run
$ ^Z
$ bg
$ /challenge/run
```

## Flag: 

```
pwn.college{Mf6VKQ0WzmSoqR-6-Ncm6NAK0sR.QX3QDO0wyM1EzNzEzW}
```

### Notes:

- Suspended tasks can be resumed in background using `bg`.
- The `T` in `ps stat` means that the process is suspended due to our `Ctrl-Z`, The `S` means that the process is sleeping while waiting for input, The `R` means that it's actively running, and the `+` means that it's in the foreground.


# Challenge 8 Foregrounding Processes

Imagine that you have a backgrounded process, and you want to mess with it some more.
What do you do?
Well, you can foreground a backgrounded process with `fg` just like you foreground a suspended process!
This level will walk you through that!

## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` which shows
```
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
```

Next the user needs to suspend the process using the command `^Z`, 
```
[1]+  Stopped                 /challenge/run
```

Next the user needs to resume the suspended process in background using the command `bg` ,
```
[1]+ /challenge/run &
```

Now the user can resume the task in foreground using the command `fg`, 
```
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{cmYiD_5VV4Ea2UQAs41weMPyUi0.QX4QDO0wyM1EzNzEzW}
```

#### Commands run:

```sh
$ /challenge/run
$ ^Z
$ bg
$ fg
```

## Flag: 

```
pwn.college{cmYiD_5VV4Ea2UQAs41weMPyUi0.QX4QDO0wyM1EzNzEzW}
```

### Notes:

- We can foreground a background task using the command `fg`.


# Challenge 9 Starting background processes

Of course, you don't have to suspend processes to background them: you can start them backgrounded right off the bat!
It's easy; all you have to do is append a `&` to the command, like so:

```sh
hacker@dojo:~$ sleep 1337 &
[1] 1771
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker      1709 Ss   bash
hacker      1771 S    sleep 1337
hacker      1782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
```

Here, `sleep` is actively running in the background, _not_ suspended.
Now it's your turn to practice!
Launch `/challenge/run` backgrounded for the flag!


## Solution:

After the terminal comes up, the user needs to invoke `/challenge/run` in background, this can be done using the command `/challenge/run &` which shows
```
Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{Y0UenrWhYnjPerMlYfIYNfef51d.QX5QDO0wyM1EzNzEzW}

[1]+  Done                    /challenge/run
```

#### Commands run:

```sh
$ /challenge/run &
```

## Flag: 

```
pwn.college{Y0UenrWhYnjPerMlYfIYNfef51d.QX5QDO0wyM1EzNzEzW}
```

### Notes:

- We can start processes in background by appending a `&` to the command.


# Challenge 10 Process Exit Codes

Every shell command, including every program and every builtin, exits with an _exit code_ when it finishes running and terminates.
This can be used by the shell, or the user of the shell (that's you!) to check if the process succeeded in its functionality (this determination, of course, depends on what the process is supposed to do in the first place).

You can access the exit code of the most recently-terminated command using the special `?` variable (don't forget to prepend it with `$` to read its value!):

```sh
hacker@dojo:~$ touch test-file
hacker@dojo:~$ echo $?
0
hacker@dojo:~$ touch /test-file
touch: cannot touch '/test-file': Permission denied
hacker@dojo:~$ echo $?
1
hacker@dojo:~$
```

As you can see, commands that succeed typically return `0` and commands that fail typically return a non-zero value, most commonly `1` but sometimes an error code that identifies a specific failure mode.

In this challenge, you must retrieve the exit code returned by `/challenge/get-code` and then run `/challenge/submit-code` with that error code as an argument.
Good luck!


## Solution:

After the terminal comes up, the user needs to invoke `/challenge/get-code` which will show
```
Exiting with an error code!
```

Next the user needs to get this exit code using the command `echo $?`, which returns
```
149
```

Now the user needs to invoke `/challenge/submit-code` with the error code as an argument, `/challenge/submit-code 149` which returns
```
CORRECT! Here is your flag:
pwn.college{Q8stJs-e1SdQVGCzbWXbbtOJbFR.QX5YDO1wyM1EzNzEzW}
```

#### Commands run:

```sh
$ /challenge/get-code
$ echo $?
$ /challenge/submit-code 149
```

## Flag: 

```
pwn.college{Q8stJs-e1SdQVGCzbWXbbtOJbFR.QX5YDO1wyM1EzNzEzW}
```

### Notes:

- We can access the exit code of the most recently-terminated command using the special `?` variable (we prepend it with `$` to read its value).
- Commands which successfully run return `0` and commands which fail return `1` or any other error code.
