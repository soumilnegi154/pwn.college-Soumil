
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

Invoked like this, `grep` will search the file for lines of text containing `SEARCH_STRING` and print them to the sh.


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

- `grep SEARCH_STRING /path/to/file` invoked like this, `grep` will search the file for lines of text containing `SEARCH_STRING` and print them to the sh.
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


# Challenge 9 moving files

You can also _move_ files around with the `mv` command.
The usage is simple:

```sh
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

This challenge wants you to move the `/flag` file into `/tmp/hack-the-planet` (do it)!
When you're done, run `/challenge/check`, which will check things out and give the flag to you.

## Solution:

After the terminal comes up, the user needs to move the `/flag` file into `/tmp/hack-the-planet`, this can be done using the command `mv /flag /tmp/hack-the-planet`.

After this the user needs to invoke the `/challenge/check` program using the command `/challenge/check`.

#### Commands run:

```sh
$ mv /flag /tmp/hack-the-planet
$ /challenge/run
```

## Flag: 

```
pwn.college{051Ucouft2yBBoZ_wkV3Rbur0OH.0VOxEzNxwyM1EzNzEzW}
```

### Notes:

- files can be moved around using the `mv` command.


# Challenge 10 hidden files

Interestingly, `ls` doesn't list _all_ the files by default.
Linux has a convention where files that start with a `.` don't show up by default in `ls` and in a few other contexts.
To view them with `ls`, you need to invoke `ls` with the `-a` flag, as so:

```sh
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

Now, it's your turn!
Go find the flag, hidden as a dot-prepended file in `/`.


## Solution:

After the terminal comes up, the user needs to change directory to root as its mentioned that the flag is hidden in `/`, this can be done using the command `cd /`, which gives the output-

```
.   .dockerenv           bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-5122098813749  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
```

since clearly the flag is in `.flag-5122098813749`, it can be read using the command `cat .flag-5122098813749`. 

#### Commands run:

```sh
$ cd /
$ cat .flag-5122098813749
```

## Flag: 

```
pwn.college{0u9TjSSbLpIEvJYRnxy_2782kKS.QXwUDO0wyM1EzNzEzW}
```

### Notes:

- `ls` doesn't list hidden files by default.
- Linux has a convention where files that start with a `.` are hidden.




# Challenge 11 An Epic Filesystem Quest

With your knowledge of `cd`, `ls`, and `cat`, we're ready to play a little game!

We'll start it out in `/`.
Normally:

```sh
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```

That's a lot of contents!
One day, you will be quite familiar with them, but already, you might recognize the `flag` file and the `challenge` directory.

In this challenge, I have *hidden the flag*!
Here, you will use `ls` and `cat` to follow my breadcrumbs and find it!
Here's how it'll work:

0. Your first clue is in `/`. Head on over there.
1. Look around with `ls`. There'll be a file named HINT or CLUE or something along those lines!
2. `cat` that file to read the clue!
3. Depending on what the clue says, head on over to the next directory (or don't!).
4. Follow the clues to the flag!

Good luck!


## Solution:

After the terminal comes up, the user needs to read the hints and follow the directories which are given-

- it starts with root directory, this can be done using the command `cd /` `ls` which outputs
```
CLUE  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin   challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
```
- the user needs to read the `CLUE` file, this can be done using the command `cat CLUE` which outputs
```
Tubular find!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/TeX/SansSerif

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
- the user needs to get the hint from the next clue without `cd`ing, this can be done using the command `ls  /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/TeX/SansSerif` which outputs
```
Bold  Italic  MESSAGE-TRAPPED  Regular
```
- the user needs to read the `MESSAGE-TRAPPED` file, this can be done using the command `cat /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/TeX/SansSerif/MESSAGE-TRAPPED` which outputs
```
Lucky listing!
The next clue is in: /usr/share/icons/Adwaita/8x8/emblems

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```
- the user needs to get the hint from the next clue which is hidden, this can be done using the command `ls /usr/share/icons/Adwaita/8x8/emblems -a` which outputs
```
.  ..  .TEASER  emblem-readonly.png  emblem-unreadable.png
```
- the user needs to read the `.TEASER` file, this can be done using the command `cat /usr/share/icons/Adwaita/8x8/emblems/.TEASER` which outputs
```
Lucky listing!
The next clue is in: /usr/share/racket/pkgs/images-lib/images/private/latent-contract
```
- the user needs to get the hint from the next clue which can be done using the command `ls /usr/share/racket/pkgs/images-lib/images/private/latent-contract` which outputs
```
TRACE  compiled  defthing.rkt
```
- the user needs to read the `TRACE` file which can be done using the command `cat /usr/share/racket/pkgs/images-lib/images/private/latent-contract/TRACE` which outputs
```
Yahaha, you found me!
The next clue is in: /usr/share/doc/liberror-perl/examples

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```
- the user needs to get the hint from the next clue by `cd`ing into the directory, this can be done using the command `cd /usr/share/doc/liberror-perl/examples` `ls` which outputs
```
DISPATCH  example.pl  next-in-loop  warndie.pl
```
- the user needs to read the `DISPATCH` file which can be done using the command `cat DISPATCH` which outputs
```
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/drivers/scsi/ufs
```
- the user needs to get the hint from the next clue using the command `ls /opt/linux/linux-5.4/drivers/scsi/ufs` which outputs
```
Kconfig            tc-dwc-g210-pltfrm.c  ufs-mediatek.c  ufs-sysfs.h   ufshcd-dwc.c     ufshcd.c
LEAD               tc-dwc-g210.c         ufs-mediatek.h  ufs.h         ufshcd-dwc.h     ufshcd.h
Makefile           tc-dwc-g210.h         ufs-qcom.c      ufs_bsg.c     ufshcd-pci.c     ufshci-dwc.h
cdns-pltfrm.c      ufs-hisi.c            ufs-qcom.h      ufs_bsg.h     ufshcd-pltfrm.c  ufshci.h
tc-dwc-g210-pci.c  ufs-hisi.h            ufs-sysfs.c     ufs_quirks.h  ufshcd-pltfrm.h  unipro.h
```
- the user needs to read the `LEAD` file which can be done using the command `cat /opt/linux/linux-5.4/drivers/scsi/ufs/LEAD` which outputs
```
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/tools/usb/usbip/src

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
- the user needs get the hint from the next clue without `cd`ing, this can be done using the command `ls /opt/linux/linux-5.4/tools/usb/usbip/src` which outputs
```
HINT-TRAPPED  usbip.c  usbip_attach.c  usbip_detach.c  usbip_network.c  usbip_port.c    usbipd.c  utils.h
Makefile.am   usbip.h  usbip_bind.c    usbip_list.c    usbip_network.h  usbip_unbind.c  utils.c
```
- the user needs to read the `HINT-TRAPPED` file which can be done using the command `cat /opt/linux/linux-5.4/tools/usb/usbip/src/HINT-TRAPPED` which outputs
```
Lucky listing!
The next clue is in: /usr/share/racket/pkgs/gui-lib/mrlib/compiled

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```
- the user needs to get the hint from the next clue which is hidden, this can be done using the command `ls /usr/share/racket/pkgs/gui-lib/mrlib/compiled -a` which outputs
```
.                                gif_rkt.zo                      name-message_rkt.zo
..                               graph_rkt.dep                   path-dialog_rkt.dep
.POINTER                         graph_rkt.zo                    path-dialog_rkt.zo
aligned-pasteboard_rkt.dep       hierlist_rkt.dep                plot_rkt.dep
aligned-pasteboard_rkt.zo        hierlist_rkt.zo                 plot_rkt.zo
arrow-toggle-snip_rkt.dep        image-core-wxme_rkt.dep         snip-canvas_rkt.dep
arrow-toggle-snip_rkt.zo         image-core-wxme_rkt.zo          snip-canvas_rkt.zo
bitmap-label_rkt.dep             image-core_rkt.dep              switchable-button_rkt.dep
bitmap-label_rkt.zo              image-core_rkt.zo               switchable-button_rkt.zo
cache-image-snip_rkt.dep         include-bitmap_rkt.dep          syntax-browser_rkt.dep
cache-image-snip_rkt.zo          include-bitmap_rkt.zo           syntax-browser_rkt.zo
click-forwarding-editor_rkt.dep  info_rkt.dep                    tab-choice_rkt.dep
click-forwarding-editor_rkt.zo   info_rkt.zo                     tab-choice_rkt.zo
close-icon_rkt.dep               interactive-value-port_rkt.dep  terminal_rkt.dep
close-icon_rkt.zo                interactive-value-port_rkt.zo   terminal_rkt.zo
expandable-snip_rkt.dep          matrix-snip_rkt.dep             text-string-style-desc_rkt.dep
expandable-snip_rkt.zo           matrix-snip_rkt.zo              text-string-style-desc_rkt.zo
gif_rkt.dep                      name-message_rkt.dep
```
- the user needs to read the `.POINTER` file which can be done using the command `cat /usr/share/racket/pkgs/gui-lib/mrlib/compiled/.POINTER` which outputs
```
Lucky listing!
The next clue is in: /opt/kropr/src/bin

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```
- the user needs to get the hint from the next clue by `cd`ing, this can be done using the command `cd /opt/kropr/src/bin` `ls` which outputs
```
ALERT  ropr.rs
```
- the user needs to read the `ALERT` file, this can be done using the command `cat ALERT` which outputs
```
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{MwTAej71IKlBmrdrLekQH03nP_m.QX5IDO0wyM1EzNzEzW}
```


#### Commands run:

```sh
$ cd /
$ ls
$ cat CLUE
$ ls  /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/TeX/SansSerif
$ cat /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/TeX/SansSerif/MESSAGE-TRAPPED
$ ls /usr/share/icons/Adwaita/8x8/emblems -a
$ cat /usr/share/icons/Adwaita/8x8/emblems/.TEASER
$ ls /usr/share/racket/pkgs/images-lib/images/private/latent-contract
$ cat /usr/share/racket/pkgs/images-lib/images/private/latent-contract/TRACE
$ cd /usr/share/doc/liberror-perl/examples
$ ls
$ cat DISPATCH
$ ls /opt/linux/linux-5.4/drivers/scsi/ufs
$ cat /opt/linux/linux-5.4/drivers/scsi/ufs/LEAD
$ ls /opt/linux/linux-5.4/tools/usb/usbip/src
$ cat /opt/linux/linux-5.4/tools/usb/usbip/src/HINT-TRAPPED
$ ls /usr/share/racket/pkgs/gui-lib/mrlib/compiled -a
$ cat /usr/share/racket/pkgs/gui-lib/mrlib/compiled/.POINTER
$ cd /opt/kropr/src/bin
$ ls
$ cat ALERT
```

## Flag: 

``` 
pwn.college{MwTAej71IKlBmrdrLekQH03nP_m.QX5IDO0wyM1EzNzEzW}
```

### Notes:

- practicing ls, ls -a, cat, cd commands together.


# Challenge 12 making directories

We can create files.
How about directories?
You **m**a**k**e **dir**ectories using the `mkdir` command.
Then you can stick files in there!

Watch:

```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```

Now, go forth and create a `/tmp/pwn` directory and make a `college` file in it!
Then run `/challenge/run`, which will check your solution and give you the flag!

## Solution:

After the terminal comes up, the user needs to create a `pwn` directory in `/tmp`, this can be done using the commands `cd/tmp` `mkdir pwn`.

Next the user needs to create a file `college` in `/tmp/pwn` directory, using the commands `cd ./pwn` `touch college`.

Now the user can invoke the `/challenge/run` program to get the flag, using the command `/challenge/run`.

#### Commands run:

```sh
$ cd /tmp
$ mkdir pwn
$ cd ./pwn
$ touch college
$ /challenge/run
```

## Flag: 

```
pwn.college{kmaOYwjxv4DIFtsxACjbZi1eU3m.QXxMDO0wyM1EzNzEzW}
```

### Notes:

- `mkdir` is used to create a new directory.



# Challenge 13 finding files

So now we know how to list, read, and create files.
But how do we find them?
We use the `find` command!

The `find` command takes optional arguments describing the search criteria and the search location.
If you don't specify a search criteria, `find` matches every file.
If you don't specify a search location, `find` uses the current working directory (`.`).
For example:

```sh
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```

And when specifying the search location:

```sh
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```

And, of course, we can specify the criteria!
For example, here, we filter by name:

```sh
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```

You can search the whole filesystem if you want!

```sh
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```

Now it's your turn.
I've hidden the flag in a random directory on the filesystem.
It's still called `flag`.
Go find it!

Several notes. First, there are other files named `flag` on the filesystem.
Don't panic if the first one you try doesn't have the actual flag in it.
Second, there're plenty of places in the filesystem that are not accessible to a normal user.
These will cause `find` to generate errors, but you can ignore those; we won't hide the flag there!
Finally, `find` can take a while; be patient!

## Solution:

After the terminal comes up, the user needs to search for flag file, this can be done using the command `find / -name flag`, which returns the output

```
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/tmp/tmp.4mK6TfTSUV’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/opt/busybox/busybox-1.33.2/editors/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
```

The user needs to search for the flag file among these using trial and error, in this case the file was present in `/opt/busybox/busybox-1.33.2/editors/flag` and can be read using the command `cat /opt/busybox/busybox-1.33.2/editors/flag`.

#### Commands run:

```sh
$ find / -name flag
$ cat /opt/busybox/busybox-1.33.2/editors/flag
```

## Flag: 

```
pwn.college{IWtKUdj0AfTJghoZwFFrafFrKVx.QXyMDO0wyM1EzNzEzW}
```

### Notes:

- `find` can be used to search for files or directories.
- `find` takes arguements of search criteria and search location.
- `find` matches every file. If you don't specify a search location, `find` uses the current working directory (`.`).
- we can filter by name using `find -name <name>`.


# Challenge 14 linking files

If you use Linux (or computers) for any reasonable length of time to do any real work, you will eventually run into some variant of the following situation: you want two programs to access the same data, but the programs expect that data to be in two different locations.
Luckily, Linux provides a solution to this quandary: _links_.

Links come in two flavors: _hard_ and _soft_ (also known as _symbolic_) links.
We'll differentiate the two with an analogy:

- A **hard** link is when you address your apartment using multiple addresses that all lead directly to the same place (e.g., `Apt 2` vs `Unit 2`).
- A **soft** link is when you move apartments and have the postal service automatically forward your mail from your old place to your new place.

In a filesystem, a file is, conceptually, an address at which the contents of that file live.
A hard link is an alternate address that indexes that data --- accesses to the hard link and accesses to the original file are completely identical, in that they immediately yield the necessary data.
A soft/symbolic link, instead, contains the original file name.
When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file.
In most cases, both situations result in accessing the original data, but the mechanisms are different.

Hard links sound simpler to most people (case in point, I explained it in one sentence above, versus two for soft links), but they have various downsides and implementation gotchas that make soft/symbolic links, by far, the more popular alternative.

In this challenge, we will learn about symbolic links (also known as _symlinks_).
Symbolic links are created with the `ln` command with the `-s` argument, like so:

```sh
hacker@dojo:~$ cat /tmp/myfile
This is my file!
hacker@dojo:~$ ln -s /tmp/myfile /home/hacker/ourfile
hacker@dojo:~$ cat ~/ourfile
This is my file!
hacker@dojo:~$
```

You can see that accessing the symlink results in getting the original file contents!
Also, you can see the usage of `ln -s`.
Note that the original file path comes _before_ the link path in the command!

A symlink can be identified as such with a few methods.
For example, the `file` command, which takes a filename and tells you what type of file it is, will recognize symlinks:

```sh
hacker@dojo:~$ file /tmp/myfile
/tmp/myfile: ASCII text
hacker@dojo:~$ file ~/ourfile
/home/hacker/ourfile: symbolic link to /tmp/myfile
hacker@dojo:~$
```

Okay, now you try it!
In this level the flag is, as always, in `/flag`, but `/challenge/catflag` will instead read out `/home/hacker/not-the-flag`.
Use the symlink, and fool it into giving you the flag!


## Solution:

After the terminal comes up, the user needs to create a symlink between `/flag` and `/home/hacker/not-the-flag` so that when invoking `/challenge/catflag`, it returns the contents of `/flag`.

This can be done using the command `ln -s /flag /home/hacker/not-the-flag`.

Now we can invoke catflag using the command `/challenge/catflag`.


#### Commands run:

```sh
$ ln -s /flag /home/hacker/not-the-flag
$ /challenge/catflag
```

## Flag: 

```
pwn.college{AU3vOWNOWf9Kw0_IvHSCPzo0OYg.QX5ETN1wyM1EzNzEzW}
```

### Notes:

- `ln -s` creates a symlink between 2 files.
- The original file path comes before the link path in the command.
