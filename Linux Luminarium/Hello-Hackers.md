
# Challenge 1 Intro To Commands

In this challenge, you will invoke your first command! When you type a command and hit enter, the command will be invoked, as so:

```sh
hacker@dojo:~$ whoami  
hacker
hacker@dojo:~$
```
Here, the user executed the whoami command, which simply prints the username (hacker) to the terminal. When the command terminates, the shell once again displays the prompt, ready for the next command.

## Solution:

After the terminal comes up, the user needs to invoke the ```hello``` command, which prints the flag

#### Commands run: 

```sh
$ hello
```

## Flag: 

```
pwn.college{oz8lN2MQCqBjadzrwAEf4N9CIoo.QX3YjM1wyM1EzNzEzW}
```

### Notes:

- The ```$``` at the end of the prompt signifies that hacker is not an administrative user.
- commands in Linux are case sensitive: hello is different from HELLO.

# Challenge 2 Intro To Arguments

Let's try something more complicated: a command with arguments, which is what we call additional data passed to the command. When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments. Observe:

```sh
hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
```

In this case, the command was echo, and the argument was Hello. echo is a simple command that "echoes" all of its arguments back out onto the terminal, like you see in the session above.

Let's look at echo with multiple arguments:

```sh
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
```

In this case, the command was echo, and Hello and Hackers! were the two arguments to echo. Simple!

## Solution:

After the terminal comes up, the user needs to invoke ```hello``` command with argument ```hackers```

#### Commands run: 

```sh
$ hello hackers
```

## Flag: 

```
pwn.college{IiezqSCscYdi7TSsgtQ1-ND1QGD.QX4YjM1wyM1EzNzEzW}
```

### Notes:

- When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments.
- ```echo``` is a simple command that "echoes" all of its arguments back out onto the terminal.

# Challenge 3 Command History

You're going to type a lot of commands, and typing everything from scratch can be annoying. Luckily, the shell saves a history of every command you invoke.

You can scroll through those saved commands with the up/down arrow keys. 


## Solution:

Here the flag is already in our command history (immediate previous command)

#### Commands run:

```up``` arrow to scroll to last command

## Flag: 

```
pwn.college{0-LdtND1JRDpg8iPFuCw3Sv3EST.0lNzEzNxwyM1EzNzEzW}
```

### Notes:

- We can scroll through the commands we have run using the arrow keys.




