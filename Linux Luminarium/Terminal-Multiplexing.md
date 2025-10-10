
# Challenge 1 Launching Screen

Let's dive right in!

`screen` is a program that creates virtual terminals inside your terminal.
It's somewhat like having multiple browser tabs, but for your command line!

Starting screen is super simple:

```sh
hacker@dojo:~$ screen
```

That's it!
You're now inside a screen session.
It looks _exactly_ like a terminal, but there are new capabilities there, waiting to be discovered.

For this challenge, we've hooked things up so that just launching screen will get you the flag.
Easy!

----
**NOTE:**
When you're done with your command line, type `exit` or press `Ctrl-D` to leave the screen session.
Then screen will terminate and return you to your _original_ shell.


## Solution:

After the terminal comes up, the user needs to launch screen using the command `screen`.

#### Commands run:

```sh
$ screen
```

## Flag: 

```
pwn.college{8ej3fd3BmVePmzPC6TuEluqYSXE.0VN4IDOxwyM1EzNzEzW}
```

### Notes:

- `screen` is a program that creates virtual terminals inside your terminal.
- When you're done with your command line, type `exit` or press `Ctrl-D` to leave the screen session.
Then screen will terminate and return you to your _original_ shell.


# Challenge 2 Detaching and Attaching

Now we'll start digging in with the magic of _detaching_!

Imagine you're working on something important over a remote connection, and your connection drops.
With a normal terminal (outside of this awesome dojo environment), everything's gone.
With screen, your work keeps running, and you can _reattach_ later!

You can also _detach_ on purpose, which we'll do in this challenge.
You detach by pressing `Ctrl-A`, followed by `d` (for **d**etach).
This leaves your session running in the background while you return to your normal terminal.

```sh
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$ 
```

To **r**eattach, you can use the `-r` argument to `screen`:

```sh
hacker@dojo:~$ screen -r
```

For this challenge, you'll need to:

1. Launch screen
2. Detach from it.
3. Run `/challenge/run` (this will secretly send the flag to your detached session!)
4. Reattach to see your prize

----
**FUN FACT:**
`Ctrl-A` is `screen`'s activation key for all of its shortcuts in its default configuration.
All `screen` functionality is activated by some command combination starting with `Ctrl-A`.

**HINT:**
Remember: Hold Ctrl and press A, then release both and press d.

**HINT:**
If you see `[detached from...]`, you did it right!

## Solution:

After the terminal comes up, first the user needs to launch screen using the command `screen`.

Then the user needs to detach from the screen by pressing `Ctrl-A` and `d`.

Then the user needs to invoke `/challenge/run` and reattach to the screen using the command `screen -r`.

#### Commands run:

```sh
$ screen
$ /challenge/run
$ screen -r
```

## Flag: 

```
pwn.college{8KNuX6gMPiuvX9r0vlJw_qIxoE2.0lN4IDOxwyM1EzNzEzW}
```

### Notes:

- With screen, your work keeps running, and you can _reattach_ later. We can also _detach_ on purpose by pressing `Ctrl-A`, followed by `d` (for **d**etach).
- `Ctrl-A` is `screen`'s activation key for all of its shortcuts in its default configuration.



# Challenge 3 Finding Sessions

Time for some screen detective work!

If you become an avid screen user, you will inevitably end up with multiple sessions running.
How do you find the right one to reattach to?

Well, we can list them:

```sh
hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
```

The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session.
To attach to a specific one, you use its name or its PID by giving it as an argument to `screen -r`.

```sh
hacker@dojo:~$ screen -r goodwork
```

In this challenge, we've created three screen sessions for you.
One of them contains the flag.
The other two are decoys!

You'll need to check each one until you find it.
Don't forget to detach (Ctrl-A d) before trying the next session!


## Solution:

After the terminal comes up, the user needs to list the detached screen sessions, this can be done using the command `screen -ls` which shows
```
There are screens on:
        235.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        139.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        144.session_2d4f0158ad992424    (Detached)
        147.session_5ec0d737d93e803d    (Detached)
        150.session_92f86172b6f78a4e    (Detached)
5 Sockets in /home/hacker/.screen.
```

The user needs to reattach into each screen to find the one with the flag, here its in `144.session_2d4f0158ad992424`. The user can reattach to this screen using the command `screen -r 144`.

#### Commands run:

```sh
$ screen -ls
$ screen -r 144
```

## Flag: 

```
pwn.college{84DUsDSVtqawfQ10pXaJI13PHh8.01N4IDOxwyM1EzNzEzW}
```

### Notes:

- To attach to a specific screen, we use its name or its PID by giving it as an argument to `screen -r`.


# Challenge 4 Switching Windows

Okay, so far, `screen` is just a weird sort of terminal-with-a-terminal.
But it can be much more!

Inside a single screen session, you can have multiple windows, like your browser has multiple tabs.
This can be super handy for organizing different tasks!

These windows are handled with different keyboard shortcuts, all starting with `Ctrl-A`:

- `Ctrl-A c` - Create a new window
- `Ctrl-A n` - Next window  
- `Ctrl-A p` - Previous window
- `Ctrl-A 0` through `Ctrl-A 9` - Jump directly to window 0-9
- `Ctrl-A "` - bring up a selection menu of all of the windows

For this challenge, we've set up a screen session with two windows:

- Window 0 has... well, you'll have to switch there to find out!
- Window 1 has a welcome message

Attach to the session with `screen -r`, then use one of the key combinations above to switch to Window 1.
Go get that flag!


## Solution:

After the terminal comes up, the user needs to return to the detached screen using the command `screen -r`, then the user needs to switch to window 0 to get the flag, this can be done by pressing `ctrl-A` and `0` which gives 
```

hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{coA1DPZfabFXC4im8Zf4ha14DJ1.0FO4IDOxwyM1EzNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{coA1DPZfabFXC4im8Zf4ha14DJ1.0FO4IDOxwyM1EzNzEzW}
hacker@terminal-multiplexing~switching-windows:~$ - `Ctrl-A 0` through `Ctrl-A 9` - Jump directly to window 0-9
```

#### Commands run:

```sh
$ screen -r
```

## Flag: 

```
pwn.college{coA1DPZfabFXC4im8Zf4ha14DJ1.0FO4IDOxwyM1EzNzEzW}
```

### Notes:

- Inside a single screen session we can have multiple windows.
- These windows are handled with different keyboard shortcuts, `Ctrl-A c` - Create a new window, `Ctrl-A n` - Next window, `Ctrl-A p` - Previous window, `Ctrl-A 0` through `Ctrl-A 9` - Jump directly to window 0-9, `Ctrl-A "` - bring up a selection menu of all of the windows.


# Challenge 5 Detaching and Reattaching (tmux)

Let's try the same thing with `tmux`!

`tmux` (terminal multiplexer) is screen's younger, more modern cousin.
It does all the same things but with some different key bindings.
The biggest difference?
Instead of `Ctrl-A`, tmux uses `Ctrl-B` as its command prefix.

So to detach from tmux, you press `Ctrl-B` followed by `d`.

```sh
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$ 
```

The commands also differ:
- `tmux ls` - List sessions
- `tmux attach` or `tmux a` - Reattach to session

For this challenge:
1. Launch tmux
2. Detach from it.
3. Run `/challenge/run` (this will send the flag to your detached session!)
4. Reattach to see your prize


## Solution:

After the terminal comes up, the user needs to launch tmux using the command `tmux`, the the user needs to detach using the command `ctrl-B` and `d`.

The the user needs to invoke `/challenge/run` and then reattach to tmux using the command `tmux a`.

#### Commands run:

```sh
$ tmux
$ /challenge/run
```

## Flag: 

```
pwn.college{8_Z4pgOWaJBCtpWC-oEHcVK9y9N.0VO4IDOxwyM1EzNzEzW}
```

### Notes:

- `tmux` (terminal multiplexer) is screen's younger, more modern cousin.
- Instead of `Ctrl-A`, tmux uses `Ctrl-B` as its command prefix.
- The commands also differ: `tmux ls` - List sessions, `tmux attach` or `tmux a` - Reattach to session.


# Challenge 6 Switching Windows (tmux)

Let's learn to navigate windows in tmux!

Just like screen, tmux has windows.
The key combos are different, but the concept is the same:

- `Ctrl-B c` - Create a new window
- `Ctrl-B n` - Next window  
- `Ctrl-B p` - Previous window
- `Ctrl-B 0` through `Ctrl-B 9` - Jump to window 0-9
- `Ctrl-B w` - See a nice window picker

Tmux shows your windows at the bottom in a status bar that looks like:
```
[0] 0:bash* 1:bash
```

The `*` shows your current window, and each entry also shows the process that the window was created to run.

We've created a tmux session with two windows:
- Window 0 has the flag!
- Window 1 has your warm welcome.

Go get that flag!

## Solution:

After the terminal comes up, the user needs to launch tmux using the command `tmux` and switch to window 0 by pressing `ctrl-B` and `0`.

#### Commands run:

```sh
$ tmux
```

## Flag: 

```
pwn.college{kn4RGAhXVy6NyKoxrkXb0QzVsGj.0FM5IDOxwyM1EzNzEzW}
```

### Notes:

- Just like screen, tmux has windows. The key combos are different, but the concept is the same: `Ctrl-B c` - Create a new window, `Ctrl-B n` - Next window, `Ctrl-B p` - Previous window, `Ctrl-B 0` through `Ctrl-B 9` - Jump to window 0-9, `Ctrl-B w` - See a nice window picker.
