# Linux Basics

## Linux Shortcut Key

Auto complete for directory and filenames: `Tab`

History Search: `CTRL-R`

Clear Screen: `CTRL-L`

Abandon Current Command: `CTRL-C`

## Linux Account Stuff

Create a user: `useradd -d [home_dir] [login]`

e.g. create a non-root account `useradd -d /home/fred fred`

`$` means non-root `#` means root

Changing password: `passwd [login_name]`

Changing to root:

```
sudo su - username
```

Check your current account: `whoami`

Exit your most recent su: `exit`

More details about your current user id and privileges: `id`

## File System

Move around the file system: `cd [directory-name]`

Up on level: `cd ..`

See your current path: `pwd`

Jump to your current account home directory: `cd ~`

List directory: `ls`

show all files: `ls -a`

show details: `ls -l`

Make directory: `mkdir`

Search in a local database for a program: `locate whoami`

Update the local database: `updatedb`

Find file: `find [directory_to_search] [search criteria]`

e.g. find the whoami program `find / -name whoami`

File editor: `vi, gnu-emacs, pico, mcedit, gedit`

e.g. `gedit [filename]`

head command shows the start of a file \(line is specified by -n \[n\] option\): `head -n [line] [filename]`

tail command shows the end of a file: `tail -n 2 /etc/passwd`

view output larger than a single screen: `less [test_file]`

Type `q` to quit less

other usage: `ls /dev | less`

## Running Program

See all paths: `echo $PATH`

Look at the paths where program are run from: `which ls`

Temporarily adding a path: `PATH=$PATH:/[another_directory]`

Permanently change your path: edit the `~/.bash_profile`

Looking at running processes: `ps aux` or `ps aux | less`

Task Manager: `top`

Pause a running program and get back the shell: `CTRL-Z`

To start the program again in the background: `bg`

To start the program again in the foreground: `fg`

Run a program/command and send it to the background: `find /-name ls` `&`

See jobs run in background: `jobs`

Bring one of the jobs \(default is recent job\) into the foreground: `fg [job_number]`

## Networking Stuff

Set your network interface options:

> /etc/network/interfaces

Make your changes happen \(as root\):

> service networking restart

See your interface configuration:

> ifconfig

lo is local loopback interface, eth0 is standard ethernet interface

Send ICMP Echo Request:

> ping \[IP Address\]

Looking at network usage:

> netstat -nap

Better:

> netstat -nap \| less

_Note that various TCP and UDP po1ts are shown as LISTENING. These are waiting for a connection. Others may indicate that they are ESTABLISHED. These have existing connections._

## Building Tools

untar a file

> tar xvf \[archive.tar\]

untar a file end with tar.gz or tgz

> tar xvfz \[archive . tar.gz or archive . tgz\]

1. A script is included with some tools to properly configure your system
2. make program then compiles it
3. make install command then installs the components

> . /configure make make install

_Note: Some tools don't have a "configure" script. For these, you just run the make command._

## Other command

To look for a given string in a set of files in a directory: `grep [root] *`

Manual: `man ls`

Info: `info ls`

Look for hint of an command: `whatis ifconfig`

Search for topics and the command related to that topic: `apropos network`

Equivalent to the above: `man -k network`

## Shutdown and Reboot

Shutdown and halt: `shutdown -h now`

Shutdown and reboot: `shutdown -r now` or `reboot`

