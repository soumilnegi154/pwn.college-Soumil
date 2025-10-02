
# Challenge 1 Becoming root with su

It's not just hackers that need to become `root`.
Oftentimes, you, as the owner of your computer, need to use `root` access to administer it.
Becoming `root` is a fairly common action that Linux users take, and there are two utilities that exist for this purpose: `su` and `sudo`.

In this challenge, we will cover the older one, `su` (the **s**ubstitute **u**ser command).
This is not typically used to elevate to `root` access anymore, but it is an elegant utility from a more civilized time, and we'll cover it first.

`su` is a setuid binary:

```sh
hacker@dojo:~$ ls -l /usr/bin/su
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/su
hacker@dojo:~$
```

Because it has the SUID bit set, `su` runs as `root`.
Running as `root`, it can start a `root` shell!
Of course, `su` is discerning: before allowing the user to elevate privileges to `root`, it checks to make sure that the user knows the `root` password:

```sh
hacker@dojo:~$ su
Password: 
su: Authentication failure
hacker@dojo:~$
```

This check against the `root` password is what obsoletes `su`.
Modern systems very rarely have `root` passwords, and different mechanisms (that we will learn later) are used to grant administrative access.

But THIS challenge (and only this challenge) _does_ have a `root` password.
That password is `hack-the-planet`, and you must provide it to `su` to become `root`!
Go do that, and read the flag!


## Solution:

After the terminal comes up, first the user needs to become root, this can be done using the command `su` and enterring the password `hack-the-planet`.

Now the user can access the root directory using `cd /` and read the flag using the command `cat flag`.

#### Commands run:

```sh
$ su
$ cd /
$ cat flag
```

## Flag: 

```
pwn.college{EZFFL587TPVNVXuk3DGvZqUC7X4.QX1UDN1wyM1EzNzEzW}
```

### Notes:

- Users can become root using `su` (the **s**ubstitute **u**ser command) or `sudo`.
- `su` is discerning: before allowing the user to elevate privileges to `root`, it checks to make sure that the user knows the `root` password.
- Modern systems very rarely have `root` passwords, and different mechanisms are used to grant administrative access.


# Challenge 2 Other users with su

With no arguments, `su` will start a `root` shell (after authenticating with `root`'s password).
However, you can also give a username as an argument to switch to _that_ user instead of `root`.
For example:

```sh
hacker@dojo:~$ su some-user
Password:
some-user@dojo:~$
```

Awesome!
In this level, you must switch to the `zardus` user and then run `/challenge/run`.
Zardus' password is `dont-hack-me`.
Good luck!


## Solution:

After the terminal comes up, the user needs to switch to `zardus` user using the command `su zardus` and enter the password `dont-hack-me`.

Next the user needs to invoke `/challenge/run`.

#### Commands run:

```sh
$ su zardus
$ /challenge/run
```

## Flag: 

```
pwn.college{YfFmH31R1N203jAclpmg6xRqeuG.QX2UDN1wyM1EzNzEzW}
```

### Notes:

- We can also switch to other users using `su`.


# Challenge 3 Cracking passwords

When you enter a password for `su`, it compares it against the stored password for that user.
These passwords _used_ to be stored in `/etc/passwd`, but because `/etc/passwd` is a globally-readable file, this is not good for passwords, these were moved to `/etc/shadow`.
Here is the example `/etc/shadow` from the previous level:

```sh
root:$6$s74oZg/4.RnUvwo2$hRmCHZ9rxX56BbjnXcxa0MdOsW2moiW8qcAl/Aoc7NEuXl2DmJXPi3gLp7hmyloQvRhjXJ.wjqJ7PprVKLDtg/:19921:0:99999:7:::
daemon:*:19873:0:99999:7:::
bin:*:19873:0:99999:7:::
sys:*:19873:0:99999:7:::
sync:*:19873:0:99999:7:::
games:*:19873:0:99999:7:::
man:*:19873:0:99999:7:::
lp:*:19873:0:99999:7:::
mail:*:19873:0:99999:7:::
news:*:19873:0:99999:7:::
uucp:*:19873:0:99999:7:::
proxy:*:19873:0:99999:7:::
www-data:*:19873:0:99999:7:::
backup:*:19873:0:99999:7:::
list:*:19873:0:99999:7:::
irc:*:19873:0:99999:7:::
gnats:*:19873:0:99999:7:::
nobody:*:19873:0:99999:7:::
_apt:*:19873:0:99999:7:::
systemd-timesync:*:19901:0:99999:7:::
systemd-network:*:19901:0:99999:7:::
systemd-resolve:*:19901:0:99999:7:::
mysql:!:19901:0:99999:7:::
messagebus:*:19901:0:99999:7:::
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
```

Separated by `:`s, the first field of each line is the username and the second is the password.
A value of `*` or `!` functionally means that password login for the account is disabled, a blank field means that there is no password (a not-uncommon misconfiguration that allows password-less `su` in some configurations), and the long string such as Zardus' `$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.` is the result of one-way-encrypting (hashing) Zardus' password from the last level (in this case, `dont-hack-me`).
Other fields in this file have other meanings, and you can read more about them [here](https://www.cyberciti.biz/faq/understanding-etcshadow-file/).

When you input a password into `su`, it one-way-encrypts (hashes) it and compares the result against the stored value.
If the result matches, `su` grants you access to the user!

But what if you don't know the password?
If you have the hashed value of the password, you can _crack_ it!
Even though `/etc/shadow` is, by default, only readable by root, leaks can happen!
For example, backups are often stored, unencrypted and insufficiently protected, on file servers, and this has led to countless data disclosures.

If a hacker gets their hands on a leaked `/etc/shadow`, they can start cracking passwords and wreaking havoc.
The cracking can be done via the famous [John the Ripper](https://www.openwall.com/john/), as so:

```sh
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@dojo:~$
```

Here, John the Ripper cracked Zardus' leaked password hash to find the real value of `password1337`.
Poor Zardus!

This level simulates this story, giving you a leak of `/etc/shadow` (in `/challenge/shadow-leak`).
Crack it (this could take a few minutes), `su` to `zardus`, and run `/challenge/run` to get the flag!


## Solution:

After the terminal comes up, the user needs to crack the password of user `zardus` stored in `/challenge/shadow-leak`, this can be done using [John the Ripper](https://www.openwall.com/john/) using the command `john /challenge/shadow-leak` which outputs
```
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04784g/s 278.6p/s 278.6c/s 278.6C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

Since the password to user `zardus` is `aardvark`, next the user can `su` to `zardus` using the command `su zardus` and enter the password `aardvark`.

Now the user can invoke `/challenge/run` and get the flag.

#### Commands run:

```sh
$ john /challenge/shadow-leak
$ su zardus
$ /challenge/run
```

## Flag: 

```
pwn.college{wZSp7hs4BcSRmgeIWaKzcdm9QyE.QX3UDN1wyM1EzNzEzW}
```

### Notes:

- passwords used to be stored in `/etc/passwd`, but because `/etc/passwd` is a globally-readable file, this is not good for passwords, these were moved to `/etc/shadow` (which is only readable through root). 
- A value of `*` or `!` functionally means that password login for the account is disabled, a blank field means that there is no password (a not-uncommon misconfiguration that allows password-less `su` in some configurations), and the long string such as Zardus' `$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.` is the result of one-way-encrypting (hashing) Zardus' password (in this case, `dont-hack-me`).
- If a hacker gets their hands on a leaked `/etc/shadow`, they can start cracking passwords and wreaking havoc.
The cracking can be done via the famous [John the Ripper](https://www.openwall.com/john/).


# Challenge 4 Using sudo

In the olden days, a typical Linux system had a `root` password that administrators would use to `su` to root (after logging into their account with their normal account password).
But `root` passwords are a pain to maintain, they (or their hashes!) can leak, and they don't lend themselves well to larger environments (e.g., fleets of servers).
To address this, in recent decades, the world has moved from administration via `su` to administration via `sudo` (*Fun Fact*: `sudo` originally stood for **su**peruser **do**, but has changed to "`su` 'do'", and because `su` stands for "substitute user", the current meaning of `sudo` is "substitute user, do").

Unlike `su`, which defaults to launching a shell as a specified user, `sudo` defaults to running a command as `root`:

```sh
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
```

Or, more relevant to getting flags:

```sh
hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
```

Unlike `su`, which relies on password authentication, `sudo` checks policies to determine whether the user is authorized to run commands as `root`.
These policies are defined in `/etc/sudoers`, and though it's mostly out of scale for our purposes, there are plenty of [resources](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file) for learning about this!

So, the world has moved to `sudo` and has (for the purposes of system administration) left `su` behind.
In fact, even pwn.college's Practice Mode works by giving you `sudo` access to elevate privileges!

In this level, we will give you `sudo` access, and you will use it to read the flag.
Nice and easy!

----
**NOTE:**
After this level, we will enable Privileged Mode!
When you launch a challenge in Privileged Mode (by clicking the `Privileged` button instead of the `Start` button), the resulting container will give you full `sudo` access to allow you to introspect and debug to your heart's content, but of course with a placeholder flag.


## Solution:

After the terminal comes up, the user can `cd` to root using the command `cd /`, next the user can read the flag through `sudo` access using the command `sudo cat flag`.

#### Commands run:

```sh
$ cd /
$ sudo cat flag
```

## Flag: 

```
pwn.college{cBXwaxd--z7CecImUlQO21P9r6e.QX4UDN1wyM1EzNzEzW}
```

### Notes:

- The current meaning of `sudo` is "substitute user, do".
- Unlike `su`, which defaults to launching a shell as a specified user, `sudo` defaults to running a command as `root`
- Unlike `su`, which relies on password authentication, `sudo` checks policies to determine whether the user is authorized to run commands as `root`. These policies are defined in `/etc/sudoers`.
