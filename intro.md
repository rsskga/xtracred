# Intro to system & environment maintenance

* hardware
  * main memory = storage for 0s and 1s
    * each 0 or 1 = bit
    * all input/output from peripheral devices flows through main memory
    * state = particular arrangement of bits
    * image = a particular physical arrangement of bits
  * processor (CPU)
    * operates i/o on memory
  * disks
  * network interfaces/ports
* kernel = big collection of bits
  * core of the operating system
  * software residing in memory that instructs the CPU
  * manages hardware - interfaces between the hardware and running programs
  * runs in `kernel mode`
  * unrestricted access to `kernel space` (CPU and RAM)
  * parts
  *  process management
    * sets which processes are allowed to use CPU
    * handles starting, pausing, resuming, terminating processes
    * handles context switching amongst cores and processes
    * multitasking appears as simultaneous running processes
    * actually, time slices
  * memory management
    * which is allocated, shared, and free
    * quarantines memory space for itself
    * allocates to each process
    * shares amongst processes except for private memory
    * memory management unit (MMU) enables virtual memory
  * device drivers
  * system calls a.k.a. syscalls
    * perform specific tasks that a user process alone cannot
      * i.e., opening, reading, and writing files
      * fork()
      * exec(program)
* (user) processes = big collection of bits
  * runs in `user mode`
  * access restricted to `user space` (safe CPU ops and a subset of RAM)
  * parts
    * graphical user interface (GUI)
    * servers
    * shell
  * groups
    * sets of users with common file access and permissions
  * users
    * root = superuser with unlimited permissions
      * with great power comes great responsibility
      * use with caution and only when absolutely necessary
    * root access = administrator who can operate as root

# [MacOS Shell Management](https://support.apple.com/en-us/HT208050)
## How to change your default shell
### From Users & Groups preferences
1. Choose Apple menu  > System Preferences, then click Users & Groups.
1. Click the lock , then enter your account name and password.
1. Ctrl-click username in the list, then choose Advanced Options.
1. Choose a shell from the ”Login shell” menu, then click OK to save.

![MacOS System Preferences][img-pref]

### From the command line:
View list of available shells: `cat /etc/shells`

Use `chsh` command with any available shell, i.e.:
* `chsh -s /bin/bash`
* `chsh -s /bin/zsh`

## How to use a different shell without changing the default
1. Open Terminal, then choose Terminal > Preferences.
1. From the General pane, select ”Command (complete path).”
1. In the field, enter an available shell path from `cat /etc/shells`.

![Terminal Preferences][img-term]

If you invoke the bash shell while macOS Catalina is configured to use a
 different shell, you'll see a message that the default interactive
 shell is now zsh. To silence this warning, you can add this command to
 ~/.bash_profile or ~/.profile:
`export BASH_SILENCE_DEPRECATION_WARNING=1`

## How to switch to a zsh profile and prompt
If you're using a bash profile, such as to set environment variables,
aliases, or path variables, you should switch to using a zsh equivalent.
For example:
* .zprofile == .bash_profile and runs at login, including over SSH
* .zshrc == .bashrc and runs for each new Terminal session

If you're using `.profile` (a POSIX-compliant profile), you can make
zsh automatically read its settings by adding this to `.zprofile`:
`[[ -e ~/.profile ]] && emulate sh -c 'source ~/.profile'`

You can also move some settings from a bash profile to a zsh profile
without modification. For example, to set environment variables:
`export MY_SETTING=1`

## How to test your shell scripts
To test script compatibility with Bourne-compatible shells in macOS
Catalina, you can change `/var/select/sh` to `/bin/bash`, `/bin/dash`,
or `/bin/zsh`. If you change `/var/select/sh` to a shell other than
bash, scripts that make use of bashisms may not work properly.

zsh can be made to emulate sh by executing `zsh --emulate sh`.

# CLI - Useful Commands

## Unix/Linux
* keyboard shortcuts
  * `q` (quit or exit)
  * `cmd+k` or `clear` (clear shell screen)
* navigation & orientation
  * `pwd` (print working directory = where am i?)
  * `open .` (open working directory in finder)
  * `whoami` (which user am i logged in as?)
  * `cd` (change directory)
  * `cd ..` (go up to parent directory)
  * `cd ~` (go to users home directory)
  * `cd /` (go to root directory)
  * `cd -` (go to previous location)
  * `cd /Users/rainagustafson` (absolute path example)
  * `cd Users/rainagustafson` (relative path example)
  * `ls` (list contents of current directory)
  * `ls -la` (list contents of current directory including invisibles)
* working with applications
  * `echo $PATH` (print the PATH var = known locations of executables)
  * `man open` (show documentation)
  * `which conda` (location of executable)
  * `conda --version` (print version - this flag varies by application)
* working with files & streams
  * `mkdir project` (create a directory called 'project')
  * `touch file.txt` (create a file called 'file.txt')
  * `cat file.txt` (print file contents)
  * `mv file.txt project` (move file to project directory)
  * `cp project/file.txt .` (copy from project to working directory)
  * `diff file.txt project/file.txt` (compare two files)
  * `rm file.txt` (delete 'file.txt')
  * `rm -rf project` (delete 'project' directory)
* working with permissions
  * chmod
* misc
  * symlinks
* `pipenv install twine` vs. `pipenv install -d twine`

> TODO: Amer, put these in any order you like
## Windows
* help
* where
* cd / chdir
* dir
* mkdir
* copy
* move
* del
* cd
* ren file or folder
* cls
* $APP --version
* rmdir myFolder
* more thisfile.txt
* echo some-text > fileName(.txt)
* fc

# Future Lessons

* More commands & shell text editors
* More on Github work flows
  * [Code review](https://github.com/features/code-review/)
  * Branch management
  * Git hooks
* SQL
  * TablePlus alternative
* Docker

[img-pref]: https://support.apple.com/library/content/dam/edam/applecare/images/en_US/macos/Mojave/macos-mojave-system-prefs-users-groups-advanced-login-shell.jpg
[img-term]: https://support.apple.com/library/content/dam/edam/applecare/images/en_US/macos/Mojave/macos-mojave-terminal-preferences-general-shells.jpg
