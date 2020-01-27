# Intro to system & environment maintenance

Learning Objectives
* Develop a high-level perspective on your system
* Become comfortable working on the command line
* Prepare for future DS projects
  * Deploying to Heroku
  * Running Docker

~~Before Lecture  
Live Lecture Task  
Assignment  
Resources and Stretch Goals~~

<img alt="CPU" width="500" src="https://cdn.pixabay.com/photo/2014/08/22/22/13/cpu-424812_1280.jpg">

* hardware
  * main memory = storage for 0s and 1s
    * each 0 or 1 = [bit](https://en.wikipedia.org/wiki/Bit)
    * all [input/output](https://en.wikipedia.org/wiki/Input/output) from [peripheral devices](https://en.wikipedia.org/wiki/Peripheral) flows through main memory
    * [state](https://en.wikipedia.org/wiki/State_(computer_science)) = particular arrangement of bits
    * image ([system](https://en.wikipedia.org/wiki/Disk_image) and [disk](https://en.wikipedia.org/wiki/System_image)) = a particular physical arrangement of bits
  * processor [(CPU)](https://en.wikipedia.org/wiki/Central_processing_unit)
    * operates i/o on memory
  * disks
  * network interfaces/ports
* [kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system)) = big collection of bits
  * core of the operating system
  * software residing in memory that instructs the CPU
  * manages hardware - interfaces between the hardware and running programs
  * runs in `kernel mode`
  * unrestricted access to `kernel space` (CPU and RAM)
  * parts
    * process management
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
Default prompt styles:  
`$` prompt = bash  
`%` prompt = zsh

```
The default interactive shell is now zsh. To update your account to use
zsh, please run `chsh -s /bin/zsh`. For more details, please visit
https://support.apple.com/kb/HT208050.
```

## Why did Apple change the default MacOS shell?
[According the Armin Briegel](https://scriptingosx.com/2019/06/moving-to-zsh/),
it's an open source licensing issue. I highly recommend reading this article. He also describes the process of
[manually downloading and installing a newer version of bash](https://scriptingosx.com/2019/02/install-bash-5-on-macos/) and notes
that custom bash installations reside in a different directory, usually
`/usr/local/bin/bash`.

Others claim that [zsh is better](http://zpalexander.com/switching-to-zsh/) and share a slide deck on the history of shells.

## How to change your default shell
### From Users & Groups preferences
1. Choose Apple menu  > System Preferences, then click Users & Groups.
1. Click the lock , then enter your account name and password.
1. Ctrl-click username in the list, then choose Advanced Options.
1. Choose a shell from the ”Login shell” menu, then click OK to save.

<img alt="MacOS System Preferences" width="500" src="https://support.apple.com/library/content/dam/edam/applecare/images/en_US/macos/Mojave/macos-mojave-system-prefs-users-groups-advanced-login-shell.jpg">

### From the command line:
View list of available shells: `cat /etc/shells`

Use `chsh` command with any available shell, i.e.:
* `chsh -s /bin/bash`
* `chsh -s /bin/zsh`

## How to use a different shell without changing the default
### From Terminal preferences
1. Open Terminal, then choose Terminal > Preferences.
1. From the General pane, select ”Command (complete path).”
1. In the field, enter an available shell path from `cat /etc/shells`.

<img alt="Terminal Preferences" width="500" src="https://support.apple.com/library/content/dam/edam/applecare/images/en_US/macos/Mojave/macos-mojave-terminal-preferences-general-shells.jpg">

### From the command line:
`zsh` (creates a subshell - i.e. temporary shell)
`exit` (leave the subshell)

If you invoke the bash shell while macOS Catalina is configured to use a
 different shell, you'll see a message that the default interactive
 shell is now zsh. To silence this warning, you can add this command to
 ~/.bash_profile or ~/.profile:
`export BASH_SILENCE_DEPRECATION_WARNING=1`

##

## How to switch to a default zsh profile and prompt
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
Set/reset the shebang in shell scripts.
`#!/bin/zsh.`

To test script compatibility with Bourne-compatible shells in macOS
Catalina, you can change `/var/select/sh` to `/bin/bash`, `/bin/dash`,
or `/bin/zsh`. If you change `/var/select/sh` to a shell other than
bash, scripts that make use of bashisms may not work properly.

zsh can be made to emulate sh by executing `zsh --emulate sh`.

## Moving to zsh series
[Part 1: Moving to zsh](https://scriptingosx.com/2019/06/moving-to-zsh/)  
[Part 2: Configuration Files](https://scriptingosx.com/2019/06/moving-to-zsh-part-2-configuration-files/)  
[Part 3: Shell Options](https://scriptingosx.com/2019/06/moving-to-zsh-part-3-shell-options/)  
[Part 4: Aliases and Functions](https://scriptingosx.com/2019/07/moving-to-zsh-part-4-aliases-and-functions/)  
[Part 5: Completions](https://scriptingosx.com/2019/07/moving-to-zsh-part-5-completions/)  
[Part 6: Customizing the zsh Prompt](https://scriptingosx.com/2019/07/moving-to-zsh-06-customizing-the-zsh-prompt/)  
[Part 7: Miscellanea](https://scriptingosx.com/2019/07/moving-to-zsh-part-7-miscellanea/)  
[Part 8: Scripting zsh](https://scriptingosx.com/2019/08/moving-to-zsh-part-8-scripting-zsh/)

## Random Fun Things
[Starship](https://github.com/starship/starship)

# CLI - Useful Commands

## Unix/Linux
* [keyboard shortcuts](https://support.apple.com/guide/terminal/keyboard-shortcuts-trmlshtcts/mac)
  * `tab` (select autocomplete)
  * `ctrl-c` (exit mid-command)
  * `↑` (reload last used command)
  * `ctrl-a` (move cursor to beginning of line)
  * `ctrl-e` (move cursor to end of line)
  * `ctrl-d` (delete forward)
  * `ctrl-u` (delete to beginning of line)
  * `ctrl-k` (delete to end of line)
  * `opt+→` (reposition cursor)
  * `ctrl-t` (transpose two characters)
  * `ctrl-r` (search command history)
  * `q` (quit or exit)
  * `cmd+k` or `clear` (clear shell screen)
* navigation & orientation
  * `pwd` (print working directory = where am i?)
  * `open .` (open working directory in finder)
  * `w` (list currently logged in users)
  * `whoami` (which user am i logged in as?)
  * `cd` (change directory)
  * `cd ..` (go up to parent directory)
  * `cd ~` (go to users home directory)
  * `cd /` (go to root directory)
  * `cd -` (go to previous location)
  * `cd /Users/rainagustafson` (absolute path example)
  * `cd Users/rainagustafson` (relative path example)
  * `ls` (list contents of current directory)
  * `ls -la` (list dir contents including invisibles = shift+cmd+. in Finder)
  * `ls -la ~/.z*` (using * as a wildcard is called globbing)
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
  * `curl`
  * `wget`
* working with text
  * `sort`
  * `uniq`
  * `sed`
  * `tr`
  * `grep`
* working with permissions
  * chmod
* misc
  * alias
  * history
  * symlinks
* `pipenv install twine` vs. `pipenv install -d twine`

## Windows
* `whoami` (which user am i logged in as?)
* `systeminfo` (shows system info)
* `systeminfo | findstr "Total Physical Memory"` (shows total RAM memory used)
* `time` (displays and changes time)
* `date` (displays and changes date)
* `tab` (select autocomplete)
* `ctrl-c` (exit mid-command)
* `↑` (reload last used command)
* `exit` (quit or exit)
* `help` (show documentation)
* `cd / chdir` (print working directory = where am i?)
* `cd ..` (go up to parent directory)
* `cd ~` (go to users home directory)
* `cd /` (go to root directory)
* `cd -` (go to previous location)
* `cd <path to directory>` (Change folder/directory)
* `cd /Users/rainagustafson` (absolute path example)
* `cd Users/rainagustafson` (relative path example)
* `dir` (list contents of current directory)
* `mkdir project` (create a directory called 'project')
* `echo some-text > file(.txt)` (create a file called 'file.txt' with some-text)
* `more file.txt` (print file contents)
* `file.txt` (opens the file)
* `find or findstr` (finds a string of text in a file)
* `move file.txt project` (move file to project directory)
* `del file.txt` (delete 'file.txt')
* `copy file.txt .` (copy from project to working directory)
* `fc file1.txt file2.txt` (compare two files)
* `ren file.txt or folder` (rename file or folder)
* `rmdir project` (delete 'project' directory)
* `cls` (clear shell screen)
* `code filename.py` (opens file using VSCode)
* `where conda` (location of executable)
* `conda --version` (print version - this flag varies by application)
* `curl`
* `wget`


# Future Lessons
* Dotfiles
* More commands & shell text editors
* More on Github work flows
  * [Code review](https://github.com/features/code-review/)
  * Branch management
  * Git hooks
* Heroku dev tools
* Docker
* SQL / NoSQL
  * TablePlus alternative

